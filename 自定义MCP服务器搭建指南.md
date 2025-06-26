# 自定义 MCP 服务器搭建与集成指南（亚马逊商品爬取示例）

## 1. 环境准备

1. 安装 Python 3.8 及以上。
2. 创建并激活虚拟环境（Windows 示例）：
   
   ```cmd
   python -m venv mcp-amazon-scraper
   mcp-amazon-scraper\Scripts\activate
   ```
3. 安装依赖：
   
   ```cmd
   pip install mcp playwright lxml
   D:/mcp-server/mcp-amazon-scraper/Scripts/python.exe -m playwright install
   ```

## 2. 编写 MCP 服务器脚本

在 `mcp-amazon-scraper` 目录下新建 `amazon_scraper_mcp.py`，内容如下：

```python
import os
import asyncio
from lxml import html as lxml_html
from mcp.server.fastmcp import FastMCP
from playwright.async_api import async_playwright

HTML_FILE = os.path.join(os.getenv("TMPDIR", os.getenv("TEMP", "C:\\Temp")), "amazon_product_page.html")
mcp = FastMCP("Amazon Product Scraper")

@mcp.tool()
async def fetch_page(url: str) -> str:
    print(f"Executing fetch_page for URL: {url}")
    try:
        async with async_playwright() as p:
            browser = await p.chromium.launch(headless=True)
            page = await browser.new_page()
            await page.goto(url, timeout=90000, wait_until="domcontentloaded")
            await page.wait_for_selector("body", timeout=30000)
            await asyncio.sleep(5)
            html_content = await page.content()
            with open(HTML_FILE, "w", encoding="utf-8") as f:
                f.write(html_content)
            await browser.close()
            return f"HTML content for {url} downloaded and saved successfully to {HTML_FILE}."
    except Exception as e:
        return f"Error fetching page {url}: {str(e)}"

def _extract_xpath(tree, xpath, default="N/A"):
    try:
        result = tree.xpath(xpath)
        if result:
            return result[0].text_content().strip()
        return default
    except Exception:
        return default

def _extract_price(price_str):
    if price_str == "N/A":
        return None
    try:
        cleaned_price = ''.join([c for c in price_str if c.isdigit() or c == "."])
        return float(cleaned_price)
    except (ValueError, TypeError):
        return None

@mcp.tool()
def extract_info() -> dict:
    if not os.path.exists(HTML_FILE):
        return {"error": f"HTML file not found at {HTML_FILE}. Please run fetch_page first."}
    try:
        with open(HTML_FILE, "r", encoding="utf-8") as f:
            page_html = f.read()
        tree = lxml_html.fromstring(page_html)
        title = _extract_xpath(tree, '//span[@id="productTitle"]')
        price_whole = _extract_xpath(tree, '//span[contains(@class, "a-price-whole")]')
        price_fraction = _extract_xpath(tree, '//span[contains(@class, "a-price-fraction")]')
        price_str = f"{price_whole}.{price_fraction}" if price_whole != "N/A" else _extract_xpath(tree, '//span[contains(@class,"a-offscreen")]')
        price = _extract_price(price_str)
        original_price_str = _extract_xpath(tree, '//span[@class="a-price a-text-price"]//span[@class="a-offscreen"]')
        original_price = _extract_price(original_price_str)
        rating_text = _extract_xpath(tree, '//span[@id="acrPopover"]/@title')
        rating = None
        if rating_text != "N/A":
            try:
                rating = float(rating_text.split()[0])
            except (ValueError, IndexError):
                rating = None
        reviews_text = _extract_xpath(tree, '//span[@id="acrCustomerReviewText"]')
        review_count = None
        if reviews_text != "N/A":
            try:
                review_count = int(reviews_text.split()[0].replace(",", ""))
            except (ValueError, IndexError):
                review_count = None
        availability = _extract_xpath(tree, '//div[@id="availability"]//span/text()')
        feature_elements = tree.xpath('//div[@id="feature-bullets"]//li//span[@class="a-list-item"]')
        features = [elem.text_content().strip() for elem in feature_elements if elem.text_content().strip()]
        discount = None
        if price and original_price and original_price > price:
            discount = round(((original_price - price) / original_price) * 100)
        return {
            "title": title,
            "price": price,
            "original_price": original_price,
            "discount_percent": discount,
            "rating_stars": rating,
            "review_count": review_count,
            "features": features,
            "availability": availability.strip() if isinstance(availability, str) else availability,
        }
    except Exception as e:
        return {"error": f"Error parsing HTML: {str(e)}"}

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

## 3. 启动 MCP 服务器

```cmd
D:/mcp-server/mcp-amazon-scraper/Scripts/python.exe d:/mcp-server/mcp-amazon-scraper/amazon_scraper_mcp.py
```

## 4.1 集成到 Claude Desktop 或 Cursor

### Claude Desktop

1. 打开 Claude Desktop → Settings → Developer → Edit Config。
2. 在 mcpServers 这个键下，为你的服务器添加一个配置项。请务必将 args 中的路径替换成你 amazon_scraper_mcp.py 文件的绝对路径。：
   
   ```json
   {
     "mcpServers": {
       "amazon_product_scraper": {
         "command": "python",
         "args": ["D:/mcp-server/mcp-amazon-scraper/amazon_scraper_mcp.py"]
       }
     }
   }
   ```
3. 重启 Claude Desktop，在 Claude Desktop 里，看到聊天输入区有一个小工具图标（类似锤子 🔨）。
   
   ![Claude Desktop MCP 工具图标界面](https://www.bright.cn/wp-content/uploads/2025/04/Claude-Desktop-MCP-%E5%B7%A5%E5%85%B7%E5%9B%BE%E6%A0%87%E7%95%8C%E9%9D%A2.png)
4. 聊天输入区点击工具图标，选择“Amazon Product Scraper”工具。
   
   ![Claude 可用 MCP 工具对话框 (亚马逊爬虫)](https://www.bright.cn/wp-content/uploads/2025/04/Claude-%E5%8F%AF%E7%94%A8-MCP-%E5%B7%A5%E5%85%B7%E5%AF%B9%E8%AF%9D%E6%A1%86-%E4%BA%9A%E9%A9%AC%E9%80%8A%E7%88%AC%E8%99%AB.png)

## 4.2 集成到 cline（Cursor 插件）进行 MCP 测试

### 步骤

1. 打开 Cursor → Settings → MCP。
2. 添加新 MCP 服务器，配置如下：
   
   ```json
   {
     "mcpServers": {
       "amazon_product_scraper": {
         "command": "D:/mcp-server/mcp-amazon-scraper/Scripts/python.exe",
         "args": ["D:/mcp-server/mcp-amazon-scraper/amazon_scraper_mcp.py"]
       }
     }
   }
   ```
   
   > 注意：command 字段必须为虚拟环境下的 python 路径，否则会因依赖缺失报错。
3. 保存设置。
4. 在 Cursor 聊天区点击工具图标，选择“Amazon Product Scraper”工具。
5. 先运行 `fetch_page(url)` 工具抓取页面，再运行 `extract_info()` 工具提取结构化商品信息。
6. 如看到“Processing request of type ...”等日志，说明 MCP 已正常连接。

---

## 4. 3 Cursor IDE

1. 打开 Cursor → Settings → MCP。
2. 添加新 MCP 服务器，配置路径和参数同 4.1Claude Desktop。
3. 保存后即可在聊天中调用。

## 5  使用 Cursor 的聊天功能（Cmd+l 或 Ctrl+l）。

## 6  发送一条提示，例如：“从这个亚马逊链接提取全部可用的商品信息，并将结果以 JSON 结构输出：https://www.amazon.com/dp/B09C13PZX7”

## 7 和在 Claude Desktop 中一样，Cursor 会请求授权来运行 fetch_page 和 extract_info。点击 “Run Tool” 予以批准。

## 8 Cursor 会显示交互流程，包括调用 MCP 工具的过程，最终呈现由 extract_info 工具返回的结构化 JSON 数据。

![alt text](image.png)
Cursor IDE 亚马逊商品数据提取 JSON 结果
下面是 Cursor 输出的 JSON 示例：

```json
{
 "title": "Razer Basilisk V3 Customizable Ergonomic Gaming Mouse: Fastest Gaming Mouse Switch - Chroma RGB Lighting - 26K DPI Optical Sensor - 11 Programmable Buttons - HyperScroll Tilt Wheel - Classic Black",
 "price": 39.99,
 "original_price": 69.99,
 "discount_percent": 43,
 "rating_stars": 4.6,
 "review_count": 7782,
 "features": [
 "ICONIC ERGONOMIC DESIGN WITH THUMB REST — PC gaming mouse favored by millions worldwide with a form factor that perfectly supports the hand while its buttons are optimally positioned for quick and easy access",
 "11 PROGRAMMABLE BUTTONS — Assign macros and secondary functions across 11 programmable buttons to execute essential actions like push-to-talk, ping, and more",
 "HYPERSCROLL TILT WHEEL — Speed through content with a scroll wheel that free-spins until its stopped or switch to tactile mode for more precision and satisfying feedback that's ideal for cycling through weapons or skills",
 "11 RAZER CHROMA RGB LIGHTING ZONES — Customize each zone from over 16.8 million colors and countless lighting effects, all while it reacts dynamically with over 150 Chroma integrated games",
 "OPTICAL MOUSE SWITCHES GEN 2 — With zero unintended misclicks these switches provide crisp, responsive execution at a blistering 0.2ms actuation speed for up to 70 million clicks",
 "FOCUS+ 26K DPI OPTICAL SENSOR — Best-in-class mouse sensor with intelligent functions flawlessly tracks movement with zero smoothing, allowing for crisp response and pixel-precise accuracy",
 // ... (other features)
 ],
 "availability": "In Stock"
}
```

如需扩展更多网站或功能，可参考本例继续开发自定义 MCP 工具。
