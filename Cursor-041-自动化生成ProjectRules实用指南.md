![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf8hWPyPdiafekl6fYfVVsoY1DvYccprbmdLpDRjT6br4SsfxVnj42yBee3Xx0Cu2lb2A4yzMOMMCog/0?wx_fmt=jpeg)

# Cursor 0.49.x 自动化生成 Project Rules 实用指南



## Cursor 0.49 更新概览

Cursor 0.49 版本于2025年4月15日发布，带来了一系列重要更新，完整更新内容包括：

* ** 自动化生成项目规则  ** ：核心新功能，通过对话自动创建规则文件 

* ** 更易访问的历史记录  ** ：提升历史记录的查找与使用体验 

* ** 更易于审查的代码变更  ** ：优化代码比对与审查流程 

* ** MCP支持图片  ** ：扩展了多模态能力，支持图片处理 

* ** 改进Agent对终端的控制  ** ：增强终端操作的智能化与安全性 

* ** 全局忽略文件  ** ：简化配置管理，统一忽略规则 

* ** 新模型支持  ** ：兼容更多AI模型，提升选择空间 

* ** 项目结构上下文（Beta）  ** ：更智能地理解和利用项目结构 

> 来源官方文档：  https://www.cursor.com/cn/changelog  [1]

## 快速生成 Project Rules 详解

Cursor 0.49 版本的自动生成 Project Rules 功能极大简化了创建规则的流程，特别适合希望将现有对话上下文转化为可重用规则的开发者。

### 自动生成规则的完整步骤

1. ** 在对话中使用命令生成  **
   
   * 在聊天界面中，输入  ` /Generate Cursor Rules  ` 命令 
   
   * Cursor会分析当前对话内容并提取关键上下文 
   
   * 系统会自动创建一个新规则集，包含从对话中提取的相关信息 

2. ** 规则位置与格式  **
   
   * 生成的规则将保存在项目的  ` .cursor/rules/  ` 目录下 
   
   * 规则以  ` .mdc  ` 文件格式存储，包含前置元数据和规则内容 
   
   * 自动生成的规则文件会根据内容类别智能命名 

3. ** 规则应用机制  **
   
   * 规则被设置为  ` Auto Attached  ` 时，Agent 会在处理匹配的文件时自动应用该规则，而不是之前需要设置成  ` Agent Requested  ` 。 
   
   * 规则被设置为  ` Always  ` 时，在长对话中也保持活跃，解决了之前版本可能失效的问题。 

### 实际项目测试

> 前端项目：  https://github.com/flyeric0212/wx-md  [2]
> 
> 项目规则：  https://github.com/flyeric0212/cursor-rules  [3]

#### 测试一：在已有规则的情况下进行补充

![image-20250427下午94527558](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8hWPyPdiafekl6fYfVVsoY1vqwrOaS4ic0foQ58QFhD36oYvcA9SUGuTibXAXK1G4f1nIVzPxEibia4ibg/640?wx_fmt=png&from=appmsg)
<img src="https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8hWPyPdiafekl6fYfVVsoY15G6P2BHibWx9XVXu9fS7jCfpIJrk1YsiclQNAgH8FfMiabCZoalVgThWQ/640?wx_fmt=png&from=appmsg" title="" alt="image-20250427下午94555607" width="806">

** 生成的规则文件列表  ** ：

* general.mdc：通用规范（更新后包含所有规则文件引用） 
* react.mdc：React 开发规范（已存在） 
* document.mdc：文档规范（已存在） 
* git.mdc：Git 提交规范（已存在） 
* project-structure.mdc：项目结构规范（新创建） 
* performance.mdc：性能优化规范（新创建） 
* accessibility-i18n.mdc：可访问性和国际化规范（新创建） 
* security.mdc：安全规范（新创建） 
* api-integration.mdc：API集成规范（新创建） 
* state-management.mdc：状态管理规范（新创建） 
* testing.mdc：测试规范（新创建） 

#### 测试二：拷贝原项目，删除规则后重新生成

![image-20250427下午95755055](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8hWPyPdiafekl6fYfVVsoY1SV4LaQQZn6EbaRMcn2m74icibicskVYvgK36ZdZaQI7rEYyvIW45oibtkA/640?wx_fmt=png&from=appmsg)

** 全新生成的规则文件  ** ：

* project-structure.mdc：描述项目的整体结构 
* core-components.mdc：描述项目的核心组件 
* core-functionality.mdc：描述项目的核心功能实现 
* workflow.mdc：描述项目的主要工作流程 
* tech-stack.mdc：描述项目使用的技术栈 

> 对比两次测试可以发现，不同生成方式产生的规则差异较大。在已有规则基础上生成的规则更加详细全面，而从零开始生成的规则则更专注于项目的核心架构和功能。

## 最佳实践建议

经过实际测试对比，我建议将手动编写方式和自动生成方式结合使用，形成以下工作流：

1. ** 使用手动编写方式构建基础框架  ** ：首先通过我之前提出的企业级三层规则体系，完成规则的基础框架 

2. ** 自动生成规则进行智能补充  ** ：通过  ` /Generate Cursor Rules  ` 命令基于项目上下文快速生成补充规则 

3. ** 规则验证与持续迭代优化  ** ：测试规则在不同场景下的应用效果，收集团队反馈持续优化规则，并随着项目演进定期更新规则内容 

![image-20250427下午101349176](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8hWPyPdiafekl6fYfVVsoY1QXic9wAl3eO9EGL4xnOeUrlyxzTUOT9iaWhgA9NJaF6BtOf8HwicVbasg/640?wx_fmt=png&from=appmsg)

## 注意事项

* ** 对话质量决定规则质量  ** ：在生成规则前，确保与AI进行了高质量的项目相关对话 

* ** 规则合理分类  ** ：自动生成后检查规则分类是否合理，必要时手动调整文件结构 

* ** 注意规则重叠  ** ：检查自动生成的规则是否与现有规则存在重叠或冲突 

* ** 定期更新规则  ** ：随着项目发展，定期使用自动生成功能更新规则内容 

* ** 规则粒度控制  ** ：根据项目复杂度调整规则粒度，小项目可以使用较少的规则文件 

## 总结

Cursor 0.49.x 的自动生成 Project Rules
功能显著简化了规则创建流程，尤其适合快速启动新项目或补充现有规则体系。虽然自动生成功能为快速入门提供了便利，但要达到真正的企业级项目规则效果，仍需结合手动优化和系统化的规则管理策略。

这一功能代表了 AI 辅助开发工具向更智能化、自动化方向发展的趋势，值得所有Cursor用户深入探索和应用。


