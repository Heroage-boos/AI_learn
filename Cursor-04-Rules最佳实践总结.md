![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf9Jkyo4YkkptQhiaXibUEZyCeHgYJCudYvSdNB3U2bdy73kIA4O208rFcssibQ5gdfzybicFfYhWoAOgA/0?wx_fmt=jpeg)

# Cursor Rules 最佳实践总结

使用 AI 编写代码的一大问题就是 AI 乱改，Cursor 引入了一项功能，称为 Cursor Rules。它能允许开发者规范 AI
的行为，提供更好的编码体验。让我们深入了解 Cursor Rules 是什么，以及为什么它们对现代开发工作流程至关重要。

## 什么是 Cursor Rules？

Cursor Rules 用于自定义 AI 在 Cursor
中的行为，可以视为对大型语言模型（LLM）的指令或系统提示。Cursor支持两种类型的规则设置：

1. 全局规则：在Cursor设置中的  ` Rules > User Rules  ` 设置，适用于所有项目。 

2. 项目规则：通过  ` .cursor/rules  ` 目录中的  ` .mdc  ` 文件或项目根目录的  ` .cursorrules  ` 文件设置。 

官方建议采用 Project Rules 的  ` .cursor/rules  ` 目录来管理规则文件，  ` .cursorrules  `
文件将在未来版本被废弃。

## 最佳实践

![image-20250315下午71201421](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8k2LQslURHibGcIpl8ay5GAeiahE8PKAQxVFpqtYPO2wkW9YiamQVHyDC0tdayaicvnanXiaZXm8MYMoA/640?wx_fmt=png&from=appmsg)

如果你现在采用的是  ` .cursorrules  ` 文件，可以将其分类拆分到不同的文件当中。我现在以一个实际项目，Cursor 版本为 0.47.5
为例。

### 01 通用规则

新建  ` .cursor/rules.general.mdc  `
文件，包含项目的基本信息和通用规范。设置RuleType为Always，将在所有的聊天框中应用。主要包含：技术栈、代码风格、项目结构等通用信息。

![image-20250315下午71734752](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8k2LQslURHibGcIpl8ay5GAViczztHn6ImvjjogCJlIqwYo5BFCoqaX5hKtm2NAQ9SO5OdFlJh4TRg/640?wx_fmt=png&from=appmsg)

### 02 Python 规则

该项目主要是python为主的语言，根据项目实际需求可以换成Java/React/Typescript等。新建一个  `
.cursor/rules/python.mdc  ` 文件，Rule Type 采用 Auto Attached，文件后缀为  ` *.py  `
。主要包含Python的编码规范和最佳实践等。

![image-20250315下午72042822](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8k2LQslURHibGcIpl8ay5GAT4Lb0XtibR9XaUYcsUoibpo1Q1mTfibUGNXzdshfnBVl7r9MaGFtSZVfg/640?wx_fmt=png&from=appmsg)

### 03 文档规则

新建一个  ` .cursor/rules/document.mdc  ` ，针对文档文件的规范。

![image-20250315下午72214091](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8k2LQslURHibGcIpl8ay5GAAmqSdVEpvSG1cwd8datA2j8fhSLdDHzCvKtcHDnOwSeDuOLRtASB1w/640?wx_fmt=png&from=appmsg)

### 04 Git 规则

新建一个  ` .cursor/rules/git.mdc  ` 文件，针对Git操作的规范，包含提交规范、分支管理等。

![image-20250315下午72324961](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf8k2LQslURHibGcIpl8ay5GAWpAS7UMJz7bgmwMAyZGeukHb2NuOdpA1g7LGrPqLpXQ6Oc0ZsOffqA/640?wx_fmt=png&from=appmsg)

## 最后

* 如果您是新用户，直接使用Project Rules。 
* 如果您有现有的.cursorrules文件，尽快迁移到Project Rules。 
* 使用Project Rules的高级功能来更精确地控制AI行为。 
* 将规则文件纳入版本控制，与团队共享。 
* 根据项目需求创建多个规则文件，而不是将所有规则放在一个文件中。 
* 规则需要定时进行 Review 和 改进。 

最后就算你使用了Cursor Rules，有时候它不一定会按照你的规则进行编写代码。就像我规则中写了  ` 不要自动提交git代码  `
，它有时候偶尔还是会改动完成后，你还没有accept这些文件，却被直接提交到了远程仓库。

****

****

__
