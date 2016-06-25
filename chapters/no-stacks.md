RePractise: 前后端分离 -> 全栈 -> 无栈
===

RePractise终于又迎来了新的一篇，要知道上一篇可是在半年前呢——《Repractise前端篇: 前端演进史
》。照RePractise惯例，这又是一篇超长文。

当然这也是一个神奇的标题，因为我已经想不到一个好的名字了，不过先这样吧。这篇文章算是我最近两三个月的一篇思考。在上一个项目的打杂生涯里，我开始去学习架构方面的知识，开始去接触DDD的思想。从编码到架构，再回到实际的编码中，总会有很多的灵感闪现。

这里所谓的无栈只是想说，要脱离技术栈去思考问题。

从真实世界到前后端分离
---

我们所写的代码在某种程度上都反应了真实世界的模型、行为等等。一个比较常见的模型就是：购物模型。同时， 这也是一个很好的展示前后端分离的模型。

![store-model.jpg](store-model.jpg)

（PS: 原谅我的画工）

### 便利店与售货员

对于一般的便利店来说，只有一个销售员，ta负责整个商店的一系列事务。从某种意义上来说，ta就是整个系统的核心，负责了系统的业务和事件。

一般来说在一个购买流程里，会有三个主要的人或物：

 - 售货员。一般来说，ta只会在最后的结账流程中出以及顾客询问时做出响应。
 - 货物。没啥可解释的，就是一堆模型。0
 - 顾客 。浏览商店、对比商店、blabla等等。

如果我们要构建这样一个系统，我们只需要区分出系统的各个部分，那么剩下的事情就变得很简单了。

![domain.jpg](domain.jpg)

由于整个系统仍然是相当复杂的，我们在这里只关注于用户购买的过程。

### 模型、领域、抽象

从购买过程来说，顾客所要做的事情就是：

 - 浏览、对比商品
 - 加到购物车
 - 结账、付钱 

这些商品实现上就是相当于一系列的模型及数据。在用户购买之前，我们只需要一个去获取一个个的数据接口，并展示这些数据。

后台
---

 - CRUD
 - 鉴权
 - 

前端
---

 - 事件
 - 路由
 - 模块化
 - 控制器与状态

模型与数据部分

  - 获取数据
  - 处理数据
  - 显示数据

RePractise
---