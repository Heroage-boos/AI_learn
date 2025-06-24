![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf81cKoiaTgZH7XkpYzkv9wYYWk2VUva11uHWkzhBDEgSM5icS0IgphTRQsoIHyyxzCZ1omIzVunLg0Q/0?wx_fmt=jpeg)

# Cursor 搭建高效全栈开发环境



随着AI的快速发展，越来越多的开发工具开始集成AI能力以提升开发效率。Cursor作为一款基于VS
Code的AI增强型代码编辑器，凭借其强大的AI编码助手功能和用户友好的界面，正逐渐成为开发者的得力助手。

本文将详细介绍如何在 macOS 环境下使用 Cursor 高效配置各种主流编程语言的开发环境，让开发者可以充分利用 AI 辅助编程的优势，提高开发效率。

## Cursor基础配置

在开始配置各语言环境前，建议先完成以下基础设置：

1. ** 下载安装  ** ：从  官方网站  [1]  下载最新版Cursor 

2. ** 登录账号  ** ：推荐使Google 进行快捷登录 

3. ** 导入设置  ** ：如果从VS Code迁移，可以导入现有的设置、插件和主题 

4. ** 设置全局Rules  ** ：可以参考文章进行详细配置：  [ Cursor Rules 最佳实践总结  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489450&idx=1&sn=d9df47925f101aa052abc81484cc54fd&scene=21#wechat_redirect "Cursor Rules 最佳实践总结")

这些基础配置将确保你获得最佳的Cursor使用体验。

## Python开发环境

Python 是一种解释型、高级编程语言，以简洁易读的语法著称。截至2025年，Python 持续保持编程语言流行度排行榜的前列，已经超越
JavaScript 成为 GitHub 上使用最多的语言。Python
的设计哲学强调代码可读性，使用空格缩进划分代码块，这使其成为初学者和专业人士都喜爱的语言。

### 1\. 安装

> https://www.python.org/downloads/  [2]

下载安装好后，配置你安装好的Python Path路径（不要照抄下面的路径），通过  ` vi ~/.zshrc  ` ，加入：

    export PATH="/Library/Frameworks/Python.framework/Versions/3.13/bin:$PATH"

在终端进行验证：

    $ python3 --version  
    Python 3.13.1  
    $ pip3 --version  
    pip 24.3.1 from /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages/pip (python 3.13)

如果不想要用 python3 和 pip3 命令，可以在  ` ~/.zshrc  ` 中配置：

    alias python='python3'  
    alias pip='pip3'

### 2\. 虚拟环境管理

推荐使用以下工具管理Python虚拟环境：

* ** uv  ** ：更快的包安装和环境管理工具 

* ** poetry  ** ：现代化的依赖管理和打包工具 

安装命令：

    # 安装uv  
    curl -sSf https://install.python-poetry.org | python3 -  
    
    # 安装poetry  
    pip install poetry

### 3\. Cursor 插件与配置

* Python (Microsoft)：提供语言支持 
* Python Debugger：进行 Python 调试，允许设置断点、逐行执行代码、检查变量以及执行其他基本调试任务 
* Pylance：提供静态类型检查和智能提示 
* Black Formatter：提供代码格式化 
* Pylint：代码检查 
* MypyType Checker: 类型检查 

> 参考：  https://github.com/microsoft/vscode-python/wiki/Migration-to-Python-
> Tools-Extensions  [3]

** 配置 settings.json  ** ：

    {  
      "[python]": {  
          "editor.defaultFormatter": "ms-python.black-formatter",  
          "editor.formatOnSave": true,  
      },  
      "pylint.enabled": true  
    }

** 选择项目虚拟环境  ** ：

打开命令面板（Cmd + Shift + P），搜索 "Python: Select Interpreter"，进入下面的列表进行选择。

![image-20250321下午62023387](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficicQcMWkiavvwqvHUCkLOLp3luzNtkwGqDVh3lPktJialiaFwJOibH58te8uicXyY9IF99GcfogBicP5gYA/640?wx_fmt=png&from=appmsg)

## JavaScript开发环境

JavaScript 是一种高级、解释型的编程语言，最初设计用于增强网页的交互性。如今，它已发展成为 Web 开发的基础，不仅在浏览器端使用，还通过
Node.js 扩展到服务器端开发，实现了真正的全栈开发能力。JavaScript
是一种面向对象、基于原型、动态类型的语言，支持函数式编程和现代的异步编程范式。

### 1\. 安装

node.js 安装：

    # Download and install nvm:  
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash  
    # in lieu of restarting the shell  
    \. "$HOME/.nvm/nvm.sh"  
    # Download and install Node.js:  
    nvm install 22  
    # Verify the Node.js version:  
    node -v # Should print "v22.14.0".  
    nvm current # Should print "v22.14.0".  
    # Verify npm version:  
    npm -v # Should print "10.9.2".

### 2\. 包管理工具选择

根据项目需求，选择合适的包管理工具：  **  
**

** npm  ** ：Node.js 自带，最广泛使用

** yarn  ** ：更快的依赖安装，更好的缓存机制

    npm install -g yarn

** pnpm  ** ：节省磁盘空间，高效依赖管理

    npm install -g pnpm

### 3\. TypeScript配置

TypeScript为JavaScript添加了静态类型系统，提升代码质量：

    # 全局安装  
    npm install -g typescript  
    
    # 项目初始化  
    tsc --init  
    
    # 编译TypeScript文件  
    tsc your-file.ts

### 4\. Cursor 插件与配置

* ESLint：代码质量检查 
* Prettier：代码格式化 
* JavaScript and TypeScript Nightly：启用最新的TypeScript语法 

** 配置settings.json  ** ：

    {  
      "[javascript]":{  
        "editor.tabSize":2,  
        "editor.defaultFormatter":"esbenp.prettier-vscode",  
        "editor.formatOnSave":true  
    },  
    "[typescript]":{  
        "editor.tabSize":2,  
        "editor.defaultFormatter":"esbenp.prettier-vscode",  
        "editor.formatOnSave":true  
    }  
    }

## Swift IOS/macOS开发环境

Swift 是一种强类型、多范式的编程语言，由 Apple Inc. 于2014年推出，用于开发 iOS、macOS、watchOS 和 tvOS
应用。Swift
结合了安全性、性能和软件设计模式的现代理念，提供了一种既安全又表达力强的语法。它采用自动引用计数（ARC）管理内存，防止内存泄漏和其他相关问题。

### 1\. 安装 Xcode

* 从 Mac App Store 下载最新版Xcode 
* 安装命令行工具：  ` xcode-select --install  `

### 2\. 辅助工具安装

通过以下工具增强Swift开发体验：

    # 无需打开Xcode即可构建项目  
    brew install xcode-build-server  
    
    # 美化打印 `xcodebuild` 命令输出到终端  
    brew install xcbeautify  
    
    # 高级格式化和语言功能  
    brew install swiftformat

### 3\. Cursor 插件与配置

* ** SweetPad  ** ：增强 Swift 开发体验，提供代码编译、运行和调试功能 

* ** Swift  ** ：支持 Swift 语法高亮和基本语言功能 

** SweetPad配置  ** ：

1. 安装插件后，在项目根目录创建  ` .sweetpad  ` 配置文件 

2. 设置项目特定的构建和运行参数 

> 更多sweetpad信息参考：  https://sweetpad.hyzyla.dev/docs/intro/  [4]

## Java开发环境

Java 是一种广泛使用的面向对象编程语言，以其"一次编写，到处运行"的能力著称。Java 程序在 Java
虚拟机（JVM）上运行，这使得它能够在不同的平台上运行而无需重新编译。Java
于1995年首次发布，至2025年已拥有30年的历史，但它仍然是企业应用开发的主要语言之一。

### 1\. 安装

使用  ` SDKMAN  ` 管理Java开发工具：

    # 安装SDKMAN  
    curl -s "https://get.sdkman.io" | bash  
    
    # 安装JDK  
    sdk list java  
    sdk install java 21.0.1-oracle  
    
    # 安装构建工具  
    sdk install gradle 8.7  
    sdk install maven 3.8.1  
    
    # 切换版本  
    sdk default java 21.0.1-oracle

### 2\. Cursor 插件与配置

* Extension Pack for Java：全面的Java开发支持 
* Gradle for Java：Gradle构建支持 
* Maven for Java：Maven构建支持 
* Spring Boot Extension Pack：Spring Boot应用开发支持 

** 配置settings.json  ** ：

    {  
      "java.jdt.ls.java.home":"/path/to/jdk",  
    "java.configuration.runtimes":[  
        {  
          "name":"JavaSE-21",  
          "path":"/path/to/jdk-21",  
          "default":true  
        }  
    ],  
    "[java]":{  
        "editor.formatOnSave":true  
    }  
    }

## 结语

Cursor 作为一款现代化的 AI 编辑器，为全栈开发提供了强大的支持。通过合理配置
Python、JavaScript/TypeScript、Swift和Java环境，开发者可以在一个工具中完成全栈应用的开发。

使用Cursor的几点建议：

1. ** 充分利用AI功能  ** ：使用快捷键（Cmd+K/Cmd+I）获取AI代码建议 

2. ** 定制Rules  ** ：根据项目需求设置合适的AI行为规则 

3. ** 逐步迁移  ** ：在刚开始使用时，可与熟悉的IDE（如IDEA、Xcode）配合使用 

4. ** 保持更新  ** ：Cursor更新频繁，新功能不断增加，建议及时更新 

## Cursor 系列精选阅读

探索我的更多Cursor专题文章，按学习路径排序，助您全面掌握这款AI编辑器：

** 入门篇  **

* [ 零基础入门：5步掌握Cursor AI编辑器基础操作  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247488707&idx=1&sn=2d1738ed1e91ed5220cf85a4052e9f76&scene=21#wechat_redirect "零基础入门：5步掌握Cursor AI编辑器基础操作")
* [ Cursor必学的AI交互快捷键  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489527&idx=1&sn=15d596869907716f3919a0322ae585b1&scene=21#wechat_redirect "Cursor必学的AI交互快捷键")
* [ Cursor AI提示词编写技巧总结  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489715&idx=1&sn=5f8518832e84cd06bf72f8c202fb6306&scene=21#wechat_redirect "Cursor AI提示词编写技巧总结")

** 进阶篇  **

* [ MCP 协议详解：AI 世界的"USB-C接口"  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489806&idx=1&sn=b145d3756d7d252e58efccdfa0ab651f&scene=21#wechat_redirect "MCP 协议详解：AI 世界的"USB-C接口"")
* [ Cursor 配置 MCP Server 指南  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489818&idx=1&sn=0f321f70f78db4d988d736bbd8ea5c20&scene=21#wechat_redirect "Cursor 配置 MCP Server 指南")
* [ Cursor与Git协同工作指南  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489728&idx=1&sn=37705058afd2f65f07c595f4abdcf600&scene=21#wechat_redirect "Cursor与Git协同工作指南")
* [ Cursor Rules最佳实践总结  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489450&idx=1&sn=d9df47925f101aa052abc81484cc54fd&scene=21#wechat_redirect "Cursor Rules最佳实践总结")

** 设计与开发实战  **

* [ Cursor + Flux 构建高质量本地运行的文生图 MCP 服务  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489856&idx=1&sn=9622d77159e83129885efae93f311b11&scene=21#wechat_redirect "Cursor + Flux 构建高质量本地运行的文生图 MCP 服务")
* [ Cusor 使用对话直接生成 Figma UI 设计稿  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489805&idx=1&sn=104410a3f04b1d3881f40db70b6e5ba6&scene=21#wechat_redirect "Cusor 使用对话直接生成 Figma UI 设计稿")
* [ Cursor + Figma：UI 设计稿一键转代码的高效工作流  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489831&idx=1&sn=aefd74e6c222566b4ec6f5eab274522a&scene=21#wechat_redirect "Cursor + Figma：UI 设计稿一键转代码的高效工作流")
* [ 零基础3步生成专业原型图！Cursor+Claude3.7教程  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247488719&idx=1&sn=3239316b246859a0473d9130d8898ede&scene=21#wechat_redirect "零基础3步生成专业原型图！Cursor+Claude3.7教程")
* [ Cursor中Claude 3.7 vs 3.5前端开发对比  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489482&idx=1&sn=020d1eba2b2ca1370704825e64ad4150&scene=21#wechat_redirect "Cursor中Claude 3.7 vs 3.5前端开发对比")
* [ 从0到1：完全用Cursor开发Web应用的真实体验  ](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489414&idx=1&sn=3adae9cfcbea259a1a3ff949b0adeb0f&scene=21#wechat_redirect "从0到1：完全用Cursor开发Web应用的真实体验")

* * *

#### 引用链接

` [1]  ` 官方网站:  _ https://cursor.com  
` [2]  ` :  _ https://www.python.org/downloads/  _  
` [3]  ` :  _ https://github.com/microsoft/vscode-python/wiki/Migration-to-
Python-Tools-Extensions  _  
` [4]  ` :  _ https://sweetpad.hyzyla.dev/docs/intro/  _



   
