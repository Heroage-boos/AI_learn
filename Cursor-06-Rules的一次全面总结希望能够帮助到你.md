![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKficqkGLQKv17TZ4JfEmgzL9VTia6jk9K8UksXW03vLgrs7MOPQKSlZmh7Q2ONhNKd8GZicxX3PklXgpg/0?wx_fmt=jpeg)

# Cursor Rules 的一次全面总结，希望能够帮助到你！

原创  梁波Eric  [ Eric技术圈 ](javascript:void\(0\);)

__ _ _ _ _

** 见字如面，与大家分享实践中的经验与思考。  **

大家在使用 AI 编写代码时，  最大的一个问题就是 AI 乱改  ， Cursor 有一项功能，叫做 Cursor Rules，能够在一定程度上规范 AI
的行为，让你的编程体验更好。

在我的实际使用中，前前后后原创了三篇关于 Cursor Rules
的文章，也看到很多抄袭的情况，今天在这里使用视频的方式做一下总结，给许多私信我的小伙伴进行统一的解惑。

以下每篇文章，可直接点击查看原文！

** 第一篇： [ Cursor Rules 最佳实践总结
](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489450&idx=1&sn=d9df47925f101aa052abc81484cc54fd&scene=21#wechat_redirect)
**

早期 Cursor 还没有推出细粒度的项目规则，大家用的都是.cursorrules，网上有很多工具将一堆规则都写入这个文件。
但是在我开发完成一个项目之后，发现你经常需要和 AI 进行拉扯，也就是 AI 生成的结果你不满意，反复的 Reject，然后重新生成。非常的浪费时间以及
pro 次数。

后来我就设计了：

第一，通用规则：设置成 Always，所有聊天窗口必须遵守

第二，语言规则：基于文件后缀，设置你所使用语言的编码规范和最佳实践。

第三，文档规则：生成文档的规范

第四，Git 规则：生成规范的提交记录

这样之后，基本上能够较好的满足我个人工具项目的开发。

但是，后面在进行复杂的前后端分离项目的时候，我发现第一种有些不够用了。接着就来到了：

** 第二篇： [ Cursor Rules 进阶指南：打造企业级多语言开发规范
](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247489881&idx=1&sn=660b2620dc223cf2e8976ab1fff55e12&scene=21#wechat_redirect)
**

参考此图，我设计了一个三层架构来组织 Cursor Rules，同时确保规则的可维护性和扩展性。

![image-20250402下午85703352](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficqkGLQKv17TZ4JfEmgzL9V7wWILRdBKY1ChzQD52CZeFF30dNDibrCRicobhyM2GFCA6MbpoAR0UJw/640?wx_fmt=png&from=appmsg)

这三层架构分别是：

第一，通用规则层：适用于所有项目，不受编程语言或框架的限制，这样我就可以在新增项目的时候，进行拷贝和微调。

第二，语言规则层：顾名思义，就是针对特定编程语言的规则

第三，框架规则层：一些复杂的框架，定义它们的最佳实践和规范，也是非常重要的

在完成以上这些之后，我也开源到了 github，感兴趣的小伙伴可以自由的下载、编辑。

> https://github.com/flyeric0212/cursor-rules

到了这里，基本上 Cursor Rules 已经比较完备了。

之后，cursor 推出了 0.49.x 版本，能够自动生成 Cursor Rules。这样，我就写了：

** 第三篇：Cursor 0.49.x 自动化生成 Project Rules 实用指南  **

我第一时间体验了一下该功能，使用非常简单，直接在聊天框输入/Generate Cursor Rules
命令即可。但是它要基于你有代码的情况，同时生成的很随机，这不是我想要的。

所以我的建议就是先编写我之前讲过的三层结构的基础规则，然后让 Cursor 自动生成一些补充规则文件。结合个人或者项目的实际需求，进行修改调整。

![](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficqkGLQKv17TZ4JfEmgzL9VwBnEibaPrkKzJSCMwwbR5mibKEYxmuBCIx8EDFibYRAibj3iaJOEIJJh8JQ/640?wx_fmt=png&from=appmsg)

## 总结

最后，Cursor Rules 是一个很棒的功能，如果我的实践经验能够帮助到你，记得一键三连！
