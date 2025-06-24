![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxic6A31B7EtwyZxRzC3tc0icKbK5iaJumCVlAkqiajfYMP9siaZvMMPN1TJag/0?wx_fmt=jpeg)

# 零基础入门：5步掌握Cursor AI编辑器基础操作



在当今 AI 辅助编程的浪潮中，Cursor
作为一款强大的AI编辑器，正在改变开发者的编码方式。无论你是编程新手还是经验丰富的开发者亦或者是项目经理，Cursor都能帮助你提高编码效率，减少重复劳动。本文将带你从零开始，通过5个简单步骤，快速掌握Cursor
AI编辑器的基础操作，为你的编程之旅打下坚实基础。

## 第一步：安装与基础设置

### 下载安装

访问Cursor官方网站(https://cursor.sh)下载适合你操作系统的安装包，根据安装向导完成安装过程。

![image-20250226下午93921885](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicsl7GNHiaumeicxAxfr5p8akibuR56NNtGuIUvClz5siaictU6MDWaCKTFQQ/640?wx_fmt=png&from=appmsg)

首次启动时，你需要使用邮箱注册或登录Cursor账号，这样才能使用AI功能。初次使用会有 14 天的试用期， pro 月付账号，包括无限制代码补全， 500
次快速请求，如果 500 次用完后将进入慢速排队机制。

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicRCSiaFdlwKfOyCBCKzUSyTOvpianYzosWQPMCvISZSYwB7PoUyK2icTeQ/640?wx_fmt=png&from=appmsg)

历史版本下载：https://downloader-cursor.deno.dev/

### 基础设置

如果你之前就使用 VS Code 编辑器，那么可以直接通过  ` Cursor Settings > General  ` 中导入 VS Code
的插件、设置以及快捷键，即可无缝体验 Cursor。

![image-20250226下午103450100](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicUrat4GhkqRh7MZ47LCCxo3HWrEUS3iaQ1HBVpgMiaDgJwxkuIJ6djcyA/640?wx_fmt=png&from=appmsg)

如果你是新手的话，可以先简单配置一些常用的，如：通过  ` 首选项 > 主题 > 颜色主题  ` 选择你喜欢的界面风格、在  ` 首选项 > 设置 >
文本编辑器 > 字体  ` 中调整代码字体和大小。同时通过点击扩展图标进入应用商店安装一些常用的插件，以下是一些常用插件，按需进行下载：

* Chinese (Simplified) Language Pack for Visual Studio Code：让 VS Code 显示中文语言。 
* GitLens：用于Git 管理。 
* vscode-icons：文件和文件夹的主题，可以通过后缀显示不同的图标。 
* Prettier：代码格式化工具。 
* Python：用于编写 python 代码，同时按需安装：Python Debugger、Python Poetry 等 
* Markdown Preview Github Styling：查看 Markdown 文件。 
* Draw.io Integration：查看 Drawio 文件。 
* PlantUML：绘制 plant uml 图。 
* vscode-pdf：查看 PDF 文件。 
* Office Viewer(Markdown Editor)：查看 word 、excel、markdown 文件。 

## 第二步：Cursor 布局

### 自定义布局

刚安装 Cursor 的时候，其主活动栏是横向的，可以通过  ` workbench.activityBar.orientation  `
修改活动栏方向，使用  ` workbench.sideBar.Location  ` 调整侧边栏位置，如下图：

![image-20250226下午102708558](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicw6VMkViavAHLxSNrXUnp0yjia6j0zLLb52xLjbFefLKZP1msqA9nQSvA/640?wx_fmt=png&from=appmsg)

通过以上配置就会变成之前熟悉的配方，在左侧显示并且辅助侧栏也是纵向排布的。

### AI 面板

通过快捷键  ` cmd + L  ` /  ` cmd + I  ` 或者右上角的图标可以快速打开 AI 面板。这是 Cursor
最核心和常用的地方，其中主要是  ** Chat模式  ** 和  ** Composer模式  ** 。以下是以 0.45.15版本为例。

** Chat模式  ** ：类似聊天界面，可以与AI进行对话：

* 推荐使用gpt-4o或deepseek-r1模型，综合能力强，适合做需求分析和拆解 
* 支持代码解释、问题解答等功能 

** Composer模式  ** ：专注于代码生成和编辑：

* 推荐使用 agent 模式和 Claude 3.7 模型，已达到最大的推理和代码生成能力。还有一个normal（普通模式）比较适合复杂度不高的任务。 
* 建议在需求明确和拆分清楚时，例如：先使用 Chat 模式完成需求整理，再提供给 Composer 
* 提供更精确的代码生成和修改建议 
* 代码修改后，可以先 save all 后查看运行效果，然后判断是否接受或者拒绝修改，非常好用的一个功能。 

在了解 Chat 模式和 Composer 模式之后，知道了 Chat 适合问答，可以进行本地项目问答以及基于互联网信息问答，而 Composer
则是一个代码生成器，适合处理复杂的需求场景，包括代码优化重构、新功能代码生成等。

    // Chat 场景  
    1. "帮我解释这段代码？"  
    2. "帮我检查下这段代码的问题？"  
    3. "帮我优化下这段代码的性能？"  
    4. "帮我梳理下 xxx 的需求"  
    
    // Composer 场景  
    1. "使用 React 生成一个官网"  
    2. "描述详细需求来生成代码"  
    3. "编写功能的单元测试"  
    4. "大段代码的重构"

** 上下文 context 引用  ** ：除了通过聊天框左上角的+图标添加外，还可以通过@符号进行选择，善于利用这些类型，让 Cursor
更能理解你的需求：

* FIles、Folders、Code：提供文件、文件夹和代码片段 
* Docs：类似于知识库，比较适合添加和项目相关的文档。如果想要临时添加一些知识点，可以直接@ + 链接地址，然后 add link ，并询问解析链接内容即可。 
* Git：可以基于某个 git 提交记录进行提问，例如：某次commit 的主要内容，多个 commit 之间的提交差异。 
* Notepads：可以在资源管理器中，添加一些临时笔记、上下文、对话历史记录。例如：记录一些开发思路、详细的设计需求等，推荐使用！因为 Chat 模式和 Composer 模式之间是没有上下文关联的。 
* Summarized Composers: 基于之前 AI 的历史问答记录进行回答。 
* Cursor Rules: 基于 Cursor 的自定义规则进行回答。 
* codebase：会收集整个项目中和问答相关的代码，这个需要 Codebase indexing 索引完成，新打开一个项目时可以重索引下。同时可以新增一个.cursorigore 文件让其忽略某些文件。 
* Lint errors：代码中的语法错误和潜在问题。 
* Web：联网进行搜索回答。 
* Recent Changes: 代码库最近更改作为上下文。 

![image-20250226下午103931024](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicEO7ia0E30gpPqMkjyJ6GS1jbInvWiaficzqRibcSTeoB8s9MLWqh8ctJDA/640?wx_fmt=png&from=appmsg)

使用这些符号的前提是需要提前索引好你整个项目目录，Cursor 提供了一个功能叫：CodeBase Indexing。

![image-20250227下午120217571](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicz26ztH5mzmbSp2c31rccF1U6kuda84ubIYs8TMuP4iblXw9W9cZ7ceQ/640?wx_fmt=png&from=appmsg)

** 模型列表：  ** 勾选你想要使用的大模型列表。

![image-20250227上午104828077](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicjMgTXca5G0IslJa9dA4ruB7jT4PicQthUnCNTLJqnntibOYzO1z8GXKQ/640?wx_fmt=png&from=appmsg)

## 第三步：常用快捷键

以下通过 MacOS 进行展示，如果是 Windows 将下面的 Cmd 换成 Ctrl。同时只说明和 Cursor 强关联的快捷键，其他常用快捷键参考
VS Code。

* Cmd + K：用户选择已有代码块让 AI 协助优化，用户光标在空位置则生成一段新代码。 
* Cmd + L：打开 Chat 模式，与 AI 进行对话。 
* Cmd + I：打开 Composer 模式，让 AI 进行跨文件编辑代码。 
* Cmd + .：在 Composer 模式下，打开 Agent。 
* @ 符号：通过使用“@”符号快速引用项目中的文件或代码，提高问答效率。 
* Cmd + Enter：在 Chat 模式或 Composer 模式聊天框内使用，用于让 AI 自动扫描代码库，生成更强的上下文内容，从而帮助 AI 更好地理解当前的编程环境和需求。 
* Tab：用于自动补全代码。当用户在编写代码时，Cursor AI 会根据上下文预测可能的代码完成建议，用户只需按 Tab 键即可接受这些建议。 
* Terminal Cmd + K：在终端中输入 AI 指令。 

## 第四步：AI辅助编程功能

### Tab 代码自动补全

Cursor 的自动补全功能是自动开启的，一旦在启用编辑器后，它会一直工作，并根据你最近的更改提供跨多行的代码建议。

![image-20250226下午111753780](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxic6St6WWxLwiapodfhbLoaYUPl3DBoRT9KTVOYdgu60FPtRT6pE2OckyA/640?wx_fmt=png&from=appmsg)

根据用户行为来预测代码补全，用户在编辑代码时进行智能预测和代码错误修正，以及多行编辑（一次 tab
后自动修改多行代码），光标预测（智能预测你下一次可能修改的代码的地方，然后出现 tab 图标）。

### 基础代码生成

通过注释生成代码：输入注释后，Cursor会自动生成相应的函数实现。

![image-20250226下午113015717](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicW9jz4fdAZdGXRVtSIZmtMqZvgo2KQAwffGgPqIQPciblSMFsLiaJzsZQ/640?wx_fmt=png&from=appmsg)

对于大批量代码的生成，建议在 AI 面板中描述你需要的功能，AI 会实现完整的代码，并插入到编辑器中。

### 代码解释和优化

在选中一段代码之后，Cursor 会自动弹出 Code Actions，选择 Add to Chat 后，可以使用 Chat
模型对这段代码进行问答，如：帮我解释这段代码。

![image-20250227上午105704629](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicDPZGxOXyZQHVfzpkIv54yre7JBwUMr0Tpj1JfqEt5Lc8uaA2uyqQXA/640?wx_fmt=png&from=appmsg)

也可以直接使用 Edit 模式（Cmd + K），输入指令让 Cursor 直接在代码编辑器中进行优化，修改完成后按需选择接受还是拒绝。

![image-20250227上午110416465](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicXA6P4OQnficZV3ODzm0Oywv9EVRkgQkBGeUjhU5e2yoMLPuVgW4bbfQ/640?wx_fmt=png&from=appmsg)

## 第五步：进阶技巧

### Cursor Rules（强烈推荐👍）

为什么需要 Cursor Rules 呢？每个团队、每个项目的编码风格、技术栈都不相同，为了让 Cursor AI 更好地理解你的代码习惯，避免 AI
生成不符合预期的代码。以下是你可能想要使用它的原因：

** 自定义 AI 行为  ** ：  ` .cursorrules  ` 文件有助于根据您项目的特定需求定制 AI 的响应，确保更相关和准确的代码建议。

** 一致性  ** ：通过在您的  ` .cursorrules  ` 文件中定义编码标准和最佳实践，您可以确保 AI
生成的代码与您项目的风格指南保持一致。

** 上下文感知  ** ：您可以向 AI 提供关于您项目的重要上下文，例如常用方法、架构决策或特定库，从而实现更明智的代码生成。

** 提高生产力  ** ：有了明确的规则，AI 可以生成需要较少手动编辑的代码，从而加快您的开发过程。

** 团队对齐  ** ：对于团队项目，一个共享的  ` .cursorrules  ` 文件确保所有团队成员都能获得一致的 AI
辅助，促进编码实践的协同。

** 项目特定知识  ** ：您可以包括有关项目结构、依赖关系或独特需求的信息，帮助 AI 提供更准确和相关的建议。

通过在项目根目录中创建一个  ` .cursorrules  ` 文件，您可以利用这些优势，并借助 Cursor AI 提升您的编码体验。

在 0.45 版本之后，Cursor 有两种 Rules 的方式，一种是 Project Rules（官方推荐），一种是 Global
Rules（.cursorrules 文件）。

![img](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicOP6gHJkibGOZXJJib3YwibI2JHKgQce86Ep79St4bvTYCLyVO6x4Yyurw/640?wx_fmt=png&from=appmsg)

添加 Project Rules 之后，会在  ` .cursor/rules  ` 文件夹下生成对应的文件。早期的  ` .cursorrules  `
的做法会在未来版本移出，建议采用最新的做法。

![image-20250227上午114535648](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxic0JOAWfQasjEG9CW9Oz0w69YYedUHFOFllqRB0tuMcsw2via74HAZmQA/640?wx_fmt=png&from=appmsg)

目前社区已经有很多成熟的 cursorrules 可供参考，可以先拷贝到项目中，再根据自己特定规范进行修改。

* https://github.com/PatrickJS/awesome-cursorrules 
* https://cursor.directory/ 
* https://cursorlist.com/ 
  
  

### Cursor Ignore Files

.cursorignore 文件的主要作用是告诉 Cursor 编辑器哪些文件和目录应该被忽略，不进行 AI 分析和索引。这类似于 .gitignore
的工作方式。非常建议在项目中使用该文件。

    # Ignore all files in the `dist` directory  
    dist/  
    
    # Ignore all `.log` files  
    *.log  
    
    # Ignore specific file `config.json`  
    config.json  
    
    # ignore everything  
    *  
    
    # do not ignore app  
    !app/  
    
    # do not ignore directories inside app  
    !app/*/  
    !app/**/*/  
    
    # don't ignore python files  
    !*.py

## 最后

Cursor
AI编辑器通过结合传统编辑器的强大功能和AI辅助能力，为开发者提供了一个高效的编程环境。通过本文介绍的5个基础步骤，你已经掌握了Cursor的基本操作，可以开始享受AI辅助编程带来的效率提升。

** 学习建议：  **

1. ** 循序渐进：  先熟悉基本界面和操作，再逐步探索AI功能  **
2. ** 多使用快捷键：  掌握常用快捷键可以显著提高工作效率  **
3. ** 实践结合：  将Cursor应用到实际项目中，在使用中不断学习  **
4. ** 关注更新：  Cursor团队频繁发布新功能，定期查看更新说明  **
5. ** 参与社区：  加入Cursor社区，与其他用户交流经验和技巧  **

不管你是不是程序员，都可以试着去掌握主流的 AI 编辑器，随着你对它们的深入使用，你会发现不仅是一个编辑器，更是你工作中的得力助手。

## 附录

0.46 版本更新：

![image-20250227下午35143493](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf9U9yG9KLDxwKH45GbCLicxicmIetcIOLfBQgOzjX10DNPw15xRKlpCRUiaXWLhYSBNsam6H1efrbekw/640?wx_fmt=png&from=appmsg)

Agent：新版 Cursor 的默认模式，带来更强大和统一的 AI 体验，能够支持自动 web 联网操作。

Ask：之前的 Chat 模式。

Edit：之前的 Composer 模式。

预览时标签不可点


