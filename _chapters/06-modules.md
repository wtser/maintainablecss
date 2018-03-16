---
layout: chapter
title: 模块
section: Core
permalink: /chapters/modules/
description: 学习模块和组件的区别，如何在设计者区分它们。一些模块代码例子。
---

## 什么是模块？

模块是一个不同的，独立的单元，能与其他模块结合形成更复杂的结构。

在客厅，我们可以认为 电视机，沙发和壁画是模块。这些模块一起组成了一个有用的房价。

如果我们拿走其中一个单元，其他的依然可以工作。没有电视我们也可以坐在沙发上等等。

一个网站的头部，注册表单，购物车，文章，产品列表，导航菜单等等都可以被认为是一个模块。

## 什么是组件？

模块由组件组成。 没有组件，模块是不完整的或被破坏的。

例如，沙发是由框架、装饰、腿、靠垫和靠枕组成的。所有的这一切让沙发能按照设计的功能运作。

一个 logo 模块可以是由文字，图片和链接组成，每个部分都是组件。 没有图片那么logo 就是坏了，没有链接那么logo就是不完整的。

## 模块 vs 组件

Sometimes it's hard to decide whether something should be a component or a module. For example, we might have a header containing a logo and a menu. Are these components or modules?

In a recent project it made most sense for the logo to be a component and the menu to be a module of its own. What's a header without logo? And the navigation might be moved below the header.

Nobody understands your requirements as well as you do. Through experience you'll get a feel for it. And if you get it wrong, changing from a component to a module is easy.

That's enough theory. Let's build three different modules together. In doing so, the hope is to cover most of the things we think about when writing CSS.

## 1. 创建一个 购物车 模块

我们简化一下这个 购物车 ，购物车 中的每个产品都会显示标题并可以从中移除。

购物车模板：

	<div class="basket">
	  <h1 class="basket-title">你的购物车</h1>
	  <div class="basket-item">
	      <h3 class="basket-productTitle">产品名称</h3>
          <form>
              <input type="submit" class="basket-removeButton" value="删除">
	      </form>
	  </div>
	</div>

CSS：

	.basket {}
	.basket-title {}
	.basket-item {}
	.basket-productTitle {}
	.basket-removeButton {}

## 2. 创建一个 订单合计 模块

接下来，我们会构建一个订单合计 模块。 此模块在结帐过程中显示，并与购物车有一些相似之处。 例如它有一个标题，它显示了一个产品列表。

当然，它有一个不同的界面，并且产品不能被删除。例如，没有表单和删除按钮了。

首先要解决的是购物车模板（和 CSS） 复用的问题。尽管有点相似，但是不意味着他们是一样的。

如果我们尝试将它们结合起来，这两个模块的显示逻辑和CSS覆盖问题会搞在一起。这样会把问题搞复杂，更难于维护，难于避免。

反过来，我们应该创建一个新的模块，模板如下：

	<div class="orderSummary">
	  <h2 class="orderSummary-title">订单合计</h2>
	  <div class="orderSummary-item">...</div>
	  <div class="orderSummary-item">...</div>
	</div>

CSS：

	.orderSummary {}
	.orderSummary-title {}
	.orderSummary-item {}

尽管这看起来是违反直觉的，重复有一个更好的预期。 而且，这并不是真的重复。重复指的是复制 *相同* 的东西。这两个模块虽然看来相似其实不是。

保持分离，保持简单。简单是构建可靠、可伸缩和可维护的软件最重要的部分。

## 3. 创建一个按钮模块

由于我们的购物车模块只出现在购物车页面中，所以我们没有考虑在其他地方重用它。 另外，删除按钮其实是购物车的一个组成部分，这使得跨模块的重用变得更加困难。

按钮是一个复用的好例子，在很多模块中 *潜在*。 (按钮对其本身而言并不是特别有用)

一种方式是将按钮组件升级为以下模块：

	<input class="button" type="submit" value="{%raw%}{{text}}{%endraw%}">

CSS：

	.button {}

问题在于由于内容的不同，按钮的定位、大小和间距都有细微的差别。当然还有媒体查询需要考虑。

例如，某个模块中按钮可能需要右对齐。在另一个模块中可能需要居中。

理想情况下，我们应该在*设计*阶段消除这些不一致，而不是在代码阶段去调整。但由于这并不总是可行的，而且为了举例，我们假设我们必须处理这些问题。

因此，由于这些差异，我们很难抽象出共同的规则，因为我们不想被样式覆盖折腾了。甚至糟糕到害怕更新样式规则。

为了避免这些问题，我们可以使用 mixin 或逗号分隔不影响其他内容的公共规则。例如：

	.basket-removeButton,
	.another-loginButton,
	.another-deleteButton {
      background-color: green;
      padding: 10px;
      color: #fff;
	}

注意以上只是一个例子，我们不区分 `float`, `margin` 或者 `width` 等. 这些样式会被应用到独立的按钮上：

	.basket-removeButton {
	  float: right;
	}

	.another-deleteButton {
	  margin-bottom: 10px;
	}

这似乎是明智的，因为这意味着我们可以选出这些共同的样式。 反过来，它容易被覆盖样式。但我们还有第三种选择。

想象一个结帐流程，每个页面都有一个继续按钮，并链接到前面的步骤。我们可以通过将其升级为模块来实现复用：

	<div class="checkoutActions">
	  <input class="checkoutActions-continue">
	  <a class="checkoutActions-back"></a>
	</div>

CSS：

	.checkoutActions-continue { }

	.checkoutActions-back { }

为了实现这个，我们抽象并应用了样式给 `.checkoutActions` 模块。 并且我们做到了实现的同时不影响类似的，但是不相同的按钮。

目前为止我们还未谈论按钮的多种类型的情况 (例如主要的 和 次要的 )。 我们可以使用修饰器来实现，这会在后面提到。

## 结语

一个模块，从定义上来讲，是一个可复用的 由HTML 和 CSS组成的代码块。 在一群元素能成为模块之前，我们必须先理解他们是什么和他们在使用上的区别。

这样，我们才能设计出正确的抽象。在这样做的同时，我们避免了复杂性，复杂是不可维护 CSS 的根源。
