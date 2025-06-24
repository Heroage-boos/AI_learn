![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf97sthbx6tAlibLOb5CFoQoq6Rou2OUYuicIibgH4Y5KSZOicYajzhmNenv6ZroYL1FPaBkt5cFNgaw4Q/0?wx_fmt=jpeg)

# 零基础3步生成专业原型图！Cursor+Claude3.7保姆级教程（附模板）

作为一名从后端转向前端的全栈工程师，在 UI 原型设计方面存在不足。但自从 Claude 3.7 推出后，前端开发能力和审美相较于 Claude 3.5
得到了显著提升，可以直接借助 Claude 3.7 与 Cursor 直接生成一整套 UI 设计图。

如果想要了解 Claude 3.7 Sonnet 和 Claude 3.5 Sonnect 在前端编程能力的区别，可以直接参考 github 源码和教程：

> https://github.com/flyeric0212/claude-3.5-vs-3.7-code-comparison

通过相应的提示词，可以直接生成一整套的 UX 原型设计稿，如下所示：

![pilates](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKf97sthbx6tAlibLOb5CFoQoqbE20icFwWpJ0iaSLOSo3Xl5gbeXtRt8Ft44reaUa3FP5xIlw7RsMvFCQ/640?wx_fmt=jpeg&from=appmsg)

以上操作非常简单，三步即可完成，有 Cursor 的小伙伴可以直接上手：

1. 整理好相应的提示词（可以直接参考本案例提示词，按需修改）。 
2. 在 Ask 模式（0.46 版本以下是 Chat 模式）使用 Claude 3.7 Sonnet 模型进行提问。 
3. 代码上下文过长，需要多次生成后统一汇总到一个 HTML 文件中。 

具体操作步骤如下：

第一步，整理提示词。

> 你是一名精通 UI 设计和产品规划的全栈工程师，拥有 20 年的 UX 设计经验。你的任务是帮助一位初中生用户完成一个“健身普拉提”iOS App
> 的开发。
> 
> 现在你的目标是输出一套完整的APP原型图来辅助后续的开发任务，请遵循以下原则：
> 
> \- 模拟真实用户使用普拉提类APP的真实场景和需求；
> 
> \- 结合用户需求，以产品经理的视角去规划APP的功能、页面和交互；
> 
> \- 结合产品规划，以设计师的视角去输出完整的UI/UX；
> 
> \- 引入tailwindcss来完成style样式，图片使用unsplash
> 
> \- 以上全部页面都在同一个html文件中展示。

第二步：使用 Cursor + Claude 3.7 Sonnet，在 Ask 模型中进行提问。

如果直接使用 Edit 模式进行提问，会发现因代码上下文过长导致中断，后改成 Ask 模式。

![image-20250303下午35447836](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf97sthbx6tAlibLOb5CFoQoqeYjSbEB8cRkEs4JmPJr9zeicS81qiayzKYtwYQIKQRwh0QymWN5uVjNw/640?wx_fmt=png&from=appmsg)

改为 Ask 模式后，继续提问。

![image-20250303下午35837826](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf97sthbx6tAlibLOb5CFoQoq24R7TqT35iatGiciaz88HGNIxM8PCNPcYY1MXiagVJMRGZwiawuAEGMbLZg/640?wx_fmt=png&from=appmsg)

第三步，在中断后，发送几轮“继续”之后，就可以生成多段 HTML 代码。将其拷贝到一个 HTML 文件即可。

![image-20250303下午40006475](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf97sthbx6tAlibLOb5CFoQoqaW6ukQyzU54KUmvQfNgSx9AMZpFvzgMVhEL8zkVicwwf9ZmlNM8laFQ/640?wx_fmt=png&from=appmsg)
![image-20250303下午41557157](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKf97sthbx6tAlibLOb5CFoQoqkzCQFMiczwzfAkFXVAQLU6kyZau1V06c1ygGaM6EhlGCYic2r6MCm0LA/640?wx_fmt=png&from=appmsg)

整个生成 UI 原型图的过程非常的简单，同时审美也很在线。

在提示词中并没有加入太多功能描述的前提下，Claude 3.7也能自行丰富，如果在提示词中加入更多的规则来约束的话，能更好的满足部分复杂项目的诉求。

最后，对于独立开发者来说，可以说是一个非常大的利好，能够极大的提升效率的同时，也能更好的补充不同技能之间的短板。

如果还没有开始体验 Cursor 的话，可以参考本文进行快速入门：  [ 零基础入门：5步掌握Cursor AI编辑器基础操作
](https://mp.weixin.qq.com/s?__biz=Mzk0NDI1NzI2Mw==&mid=2247488707&idx=1&sn=2d1738ed1e91ed5220cf85a4052e9f76&scene=21#wechat_redirect
"零基础入门：5步掌握Cursor AI编辑器基础操作") 。
