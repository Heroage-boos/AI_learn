![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLpX4hqw1Et8V6wgToNkBSyaqGicW9XcicTHoxKKhW9W2lp2tSskEuDPqA/0?wx_fmt=jpeg)

# 私有化部署 Dify 并快速搭建 AI 应用

__ _ _ _ _

# Dify介绍

Dify 是一个开源的 LLM 应用开发平台。其直观的界面结合了 AI 工作流、RAG
管道、Agent、模型管理、可观测性功能等，让您可以快速从原型到生产。以下是其核心功能列表：

**1\. 工作流** : 在画布上构建和测试功能强大的 AI 工作流程，利用以下所有功能以及更多功能。

**2\. 全面的模型支持** : 与数百种专有/开源 LLMs 以及数十种推理提供商和自托管解决方案无缝集成，涵盖 GPT、Mistral、Llama3
以及任何与 OpenAI API 兼容的模型。完整的支持模型提供商列表可在  此处  [1]  找到。

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyL2El5kbjEYbCtVcGctJgVQgJbO00FUZD2f0IQaMiawatVZb8bmxzAKbA/640?wx_fmt=png&from=appmsg)

**3\. Prompt IDE** : 用于制作提示、比较模型性能以及向基于聊天的应用程序添加其他功能（如文本转语音）的直观界面。

**4\. RAG Pipeline** : 广泛的 RAG 功能，涵盖从文档摄入到检索的所有内容，支持从 PDF、PPT
和其他常见文档格式中提取文本的开箱即用的支持。

**5\. Agent 智能体** : 您可以基于 LLM 函数调用或 ReAct 定义 Agent，并为 Agent 添加预构建或自定义工具。Dify 为
AI Agent 提供了50多种内置工具，如谷歌搜索、DELL·E、Stable Diffusion 和 WolframAlpha 等。

**6\. LLMOps** : 随时间监视和分析应用程序日志和性能。您可以根据生产数据和标注持续改进提示、数据集和模型。

**7\. 后端即服务** : 所有 Dify 的功能都带有相应的 API，因此您可以轻松地将 Dify 集成到自己的业务逻辑中。

Dify架构图如下：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLNqeHukyr8yBxk12J39hn81cZn4QQOM3E9sZGA0DMkYwKHy7xUIxic5Q/640?wx_fmt=png&from=appmsg)

# 功能比较

| 功能             | Dify.AI      | LangChain | Flowise | OpenAI Assistant API |
| -------------- | ------------ | --------- | ------- | -------------------- |
| 编程方法           | API + 应用程序导向 | Python 代码 | 应用程序导向  | API 导向               |
| 支持的 LLMs       | 丰富多样         | 丰富多样      | 丰富多样    | 仅限 OpenAI            |
| RAG引擎          | ✅            | ✅         | ✅       | ✅                    |
| Agent          | ✅            | ✅         | ❌       | ✅                    |
| 工作流            | ✅            | ❌         | ✅       | ❌                    |
| 可观测性           | ✅            | ✅         | ❌       | ❌                    |
| 企业功能（SSO/访问控制） | ✅            | ❌         | ❌       | ❌                    |
| 本地部署           | ✅            | ✅         | ✅       | ❌                    |

# 系统要求

    CPU >= 2 Core  
    RAM >= 4GB

如果你是MacOS系统的话，可以参考之前的文章准备一下本地的云环境： [ 打造高效MacOS系统环境
](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247484806&idx=1&sn=d8cece396c733430e0ae080d4076edfc&chksm=c3262406f451ad10f8356a45bdebb37ab7177942b2e8900280506db1fb496982b4fe32aefa28&scene=21#wechat_redirect
"打造高效MacOS系统环境")

# 本地部署

为了方便本地快速验证， **这里使用Docker Compose 运行** 。在企业或者生产环境建议采用 K8S环境部署，Dify
依赖较多的中间件，如：weaviate、redis、postgres 等，这些中间件可以采用外部已部署的应用或者容器部署，但是需要注意数据的存储。

### Docker Compose 部署

克隆 ` Dify ` 项目并运行：

    ## 克隆dify项目  
    $ git clone git@github.com:langgenius/dify.git  
    
    ## Docker Compose 运行  
    $ cd dify/docker/   
    $ docker-compose up -d

**如果官方脚本运行不起来，可以参考我调整后的Github脚本：**

    $ git clone git@github.com:flyeric0212/eric-dify-docker.git  
    $ cd eric-dify-docker  
    $ docker-compose up -d

### K8S 部署

使用Helm Chart 部署，在K8S环境部署Dify：

    ## Helm Chart by @LeoQuote  
    https://github.com/douban/charts/tree/master/charts/dify  
    
    ## Helm Chart by @BorisPolonsky  
    https://github.com/BorisPolonsky/dify-helm

### 部署验证

**使用浏览器打开如下地址：**

> http://localhost:8090/install

注意官方的是80端口，因为80端口本地被占用，所以调整成8090端口。

**查看本地存储：**

    [20:25:18] dify $ docker volume ls  
    DRIVER    VOLUME NAME  
    local     1b48b646f10961973a2abb9c885b965d7f54860dca7d7a4d42a531dc13d96b0d  
    local     446e6dfa7f4d14c2aed281af1b772495af71698bdae62fcc9140dbc57ac0bd5a  
    local     dify_app-data  
    local     dify_postgres-data  
    local     dify_redis-data  
    local     dify_weaviate-data

这样可以随时本地关闭和启动 ` Dify ` App， **数据并不会丢失。**

**注册管理员账号：**

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyL93yySsMibJnwZfK0mPa4SfbzO13pjnRA3vaxDkKN0fuUFa9hTZyiaWrA/640?wx_fmt=png&from=appmsg)

**登陆成功首页：**

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLoDzDibyrodM07E8qcqSjs5bfZWNicPuTJ67k4w5gVHDCjgulVhysoMDg/640?wx_fmt=png&from=appmsg)

# 快速构建应用

先添加模型：chatgpt以及ollama模型

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyL1HIsqMBWflWavgkBjVknJtCiaH4zkyfeAZrAff20Udvib6zraJzznXHw/640?wx_fmt=png&from=appmsg)

完成模型添加后：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLQKosq1g2OFMGQJV0AwzIdxW7DxuRwgqS7F4jibsk1mPgoDqIRdwicrIg/640?wx_fmt=png&from=appmsg)

使用模板快速使用创建一个 ` Code Interpreter ` ChatBot 应用，先使用 ` gpt-3.5-turbo ` 模型进行提问：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLl0bkCojxKrpBoteoeSFeEMlpCxiaYfDUdTuMriburAdX7XQUUrzLOJEQ/640?wx_fmt=png&from=appmsg)

再切换到本地模型 ` ollama3:8b ` 提问:

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLknic8O65heoXufVb7eh9icQRYZOzaGSSMDhYgSYww7YMJiaQXk6ozdyrQ/640?wx_fmt=png&from=appmsg)

# 添加知识库

选择本地数据源，支持非常多的文件格式，如：TXT、Markdown、PDF等。

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLlPiboaXMw6fx3clSaWiahNFOCT9Qiap0RySPjKLCqdQt89I8WQYeDPdHg/640?wx_fmt=png&from=appmsg)

文档分段和清洗：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLhlFps0ibW7QqYm6FxEpibUCZ5YRGxufGwIYewtl1N7icL6efWqHM5OLJA/640?wx_fmt=png&from=appmsg)

存储到向量数据库：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLDXVtgq5Ez0LZy5EE3wzUZlN8EUncZKLcfqEAhYck4k5GyJ3Jk2Hffw/640?wx_fmt=png&from=appmsg)

基于知识库新建应用：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLVO3bEjiaIxHDI6mickcUIjMshT0sxENKpVwCNXp95iatVE1Bk49iaMcwAw/640?wx_fmt=png&from=appmsg)

这次使用共新建了两个应用：

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8yzvAsEBwZb0u9esgicsoyLpG2VImlNNXtibGbHncoBpC5vvibWxF8o15xCsvg5h7e67HNSXBm9l2MQ/640?wx_fmt=png&from=appmsg)

# 写在最后

` Dify ` 可以切换几乎所有主流的模型，通过模板可以快速创建应用，添加各种类型的文档作为知识库，添加后端API等，相较于 ` LangChain `
需要通过 Python 代码进行开发，Dify 开箱即用，对于大部分人来说更加的友好，最重要的可以进行私有化部署。

#### 引用链接

` [1] ` 此处: _https://docs.dify.ai/getting-started/readme/model-providers

    [2]   Eric技术圈

_

dify 是一个开源平台，直接在上面创建 ai 应用，dify 帮你快速整合 llm 模型，知识库，后端 api
等，然后将应用打包发布。如果企业要定制化考虑，只想要提供出 api，自己搭建个性化应用的话，可以考虑百炼平台或者 python、Java 等源码直接开发
