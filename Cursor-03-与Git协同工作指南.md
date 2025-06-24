![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXt0CkrSY3sTQ1HJ9m5p2NkRAbiavUpaicKJYibzRzDqTVyLwyFUG4L6vIXQ/0?wx_fmt=jpeg)

# Cursor 与 Git 协同工作指南

版本控制是现代开发不可或缺的环节，而Git作为最流行的版本控制工具，其复杂命令和工作流常常让开发者头疼。Cursor AI
编辑器不仅能加速编码，还能将Git操作变得智能化，从而彻底改变你的版本控制体验。

接下来通过在项目上的 5 个 git 使用场景，来讲述如何与 AI 进行协同工作。

## 一、生成 Git 提交信息

生成高质量的 git 提交信息，是团队版本控制中非常好的一种实践。帮助开发者更容易了解每次提交所完成的功能或修复的缺陷。

### 01 Agent 聊天面板

给 AI 发出对应的指令，让其生成 Git 提交命令，同时明确指出不要自动提交。因为开启了  ` Yolo mode  ` 后 Cursor
会自动执行控制台命令。

![image-20250319下午61447057](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXtTSKTlNBlElCDh1dfK7IsEpk6AiakyRk4icVlBiby8p4ahGu0SAuU2xZ8Q/640?wx_fmt=png&from=appmsg)

最好配合  ` Cursor Rules  ` 一起使用，参考文章：  [ Cursor Rules 最佳实践总结
](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489450&idx=1&sn=d9df47925f101aa052abc81484cc54fd&scene=21#wechat_redirect
"Cursor Rules 最佳实践总结") 。

![image-20250319下午63132243](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXtsLkB1QbEvkSA3csEOibicuaPgUjFQLMSpeUico7uhXsdXP7qDubcVrC0g/640?wx_fmt=png&from=appmsg)

### 02 版本控制面板

在源代码管理界面，点击右侧的图标完成git提交信息的自动生成。

![image-20250319下午62259354](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXtChiar9fzKBPaBLeWxibyRSc90EdhyznjxicJ3MiaLklDGN70HMdicichfKwQ/640?wx_fmt=png&from=appmsg)

也可以使用自定义快捷键  ` Cmd + M  ` ，在源代码管理中自动生成 git 提交信息。

![image-20250319下午63342501](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXtia8kN8GhpbDlwJhvIpgw9RR4PXqCqFDxm3PZiaAxjmnlDTicibsoUa2HjQ/640?wx_fmt=png&from=appmsg)

## 二、智能代码审查

代码审查是保证代码质量的一种重要手段，提前发现潜在的软件缺陷，同时帮助团队成员了解系统的各个部分。

** 代码审查提示词  ** ：

    审查以下代码变更：  
    [粘贴 commit id 或 git diff 或 PR内容]  
    
    请提供：  
    1. 潜在问题或bug  
    2. 代码优化建议  
    3. 安全性考虑  
    4. 测试建议

** 效果展示  ** ：

![image-20250319下午71014780](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXt7Dx0snPnDSkKEVIhsn7ia4rIXTdfoPOjczYbsY7mgSB8CDzBibvuQLEA/640?wx_fmt=png&from=appmsg)

## 三、智能解决合并冲突

解决冲突是在多人版本协作中，必不可少的操作，非常容易引入缺陷，对于复杂的冲突，更是需要多人一起完成。  建议简单合并冲突，采用 Cursor
提供建议，人工确认执行，针对高复杂度/核心功能，人工解决。

** 冲突解决提示词  ** ：

    解决以下代码冲突。我将提供冲突内容及上下文，请分析并给出最佳解决方案。  
    
    冲突内容：  
    <<<<<<< HEAD  
    [当前分支代码]  
    =======  
    [合并分支代码]  
    >>>>>>> feature-branch  
    
    代码上下文：  
    [提供冲突文件的名称、功能描述]  
    [可选：若是分支合并的话，提供当前分支和合并分支信息]  
    
    合并目标：  
    [描述此次合并的目的，如"保留新增的用户验证功能，同时不破坏现有的错误处理逻辑"]  
    
    我需要：  
    1. 简明解释冲突产生的原因  
    2. 推荐的解决方案（完整代码）  
    3. 解决方案的简要说明  
    4. 可能需要注意的后续影响  
    
    请以代码为主，解释精简，直接提供可复制使用的解决方案。先不要执行。

## 四、复杂分支策略管理

** 分支命名提示词  ** ：

    根据以下任务生成合适的Git分支名：  
    [任务描述或需求]  
    
    请提供：  
    1. 符合最佳实践的分支名  
    2. 解释命名理由  
    3. 建议的分支起点

** 常用分支命名约定  ** ：

| 分支类型  | 命名格式             | 示例                        |
| ----- | ---------------- | ------------------------- |
| 功能分支  | feature/[描述]     | feature/user-auth         |
| 修复分支  | fix/[问题ID]-[描述]  | fix/issue-42-login-crash  |
| 发布分支  | release/[版本]     | release/v2.1.0            |
| 热修复分支 | hotfix/[版本]-[描述] | hotfix/v2.0.1-payment-fix |

如果项目中采用了 git 工作流，如：gitflow等。也可以在  ` Cursor Rules  ` 或者 命令中直接告诉 AI。

## 五、辅助生成 git 命令

对于初学者来说，大量的 git 命令可能无法记清楚，可以在 Cursor 终端使用快捷键  ` Cmd + K  ` (macos) 或者  ` Ctrl

+ K  ` (windows)，输入指令让 AI 辅助生成。

![image-20250319下午74535055](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXtKCN7ZniamW6N0we1IgEIlwVO183bOtuNKJLIs4mY0mFficnMjF2zqgWw/640?wx_fmt=png&from=appmsg)
![image-20250319下午74605985](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf91XfJvMSS6SIAmY2hEvHXtZRCL6j7iam99mPV3Gib3cbzVOJ4APe9RbWCdZZLU78VAXickpq5uRCrsQ/640?wx_fmt=png&from=appmsg)

## 最后

将Cursor与Git深度集成，能显著提升版本控制的效率和质量。AI不仅可以帮助执行常规操作，还能为复杂场景提供智能建议，减少人为错误，优化工作流程。

** 当前在多人协作的复杂项目中，建议先以分析为主，AI 操作为辅的方式。最佳方案：工具提效，人工把关。  **

### 传统 VS AI 的对比

| 操作     | 传统方式     | Cursor增强方式        |
| ------ | -------- | ----------------- |
| 提交更改   | 手动编写提交信息 | AI自动生成高质量提交描述     |
| 创建分支   | 手动指定分支名  | 基于任务自动推荐分支命名      |
| 合并代码   | 手动解决冲突   | AI辅助冲突解决与代码合并     |
| 查看历史   | 阅读原始日志   | 智能总结变更内容与影响       |
| 终端命令执行 | 查阅手册或者网站 | 自然语言辅助生成命令        |
| 代码审查   | 人工经验判断   | 人工经验+ AI 辅助建议，更全面 |
