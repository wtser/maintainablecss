---
layout: chapter
title: 语义化
section: Background
permalink: /chapters/semantics/
description: 为何给一些东西命名要基于它们是什么，而不是基于它的外观或者行为是良好架构和可维护的CSS的基础.
---

语义化 HTML 不仅仅和我们使用的元素相关。很明确我们应该使用 `<a>` 表示链接， `<table>` 表示表格数据， `<p>` 来表示段落等等。但是我们给 class 的命名就没有那么明确了。

Phil Karton 说过， *计算机科学中有两件事很难：缓存失效和 **命名***. 所以比较适合单独开一个章节来讲这个。

坦率的说，命名是编写可维护 CSS 最重要的部分。 主要有两个方式：语义化方式和非语义化方式。让我们分别讨论一下。

## 语义化 vs 非语义化

这是一些非语义化的 class：

	<div class="red pull-left pb3">
	<div class="grid row">
	<div class="col-xs-4">

非语义化 class 不表达元素本身代表**什么** ,最多他能让我们知道元素是**什么样子**的。 原子，视觉，行为和实用 class 都是非语义化 class 的表现形式。

这是一些语义化的 class：

	<div class="basket">
	<div class="product">
	<div class="searchResults">

语义化的 class 不表达它们的样式，不过没关系。那是 CSS 做的事情。语义化 class 对 HTML, CSS, Javascript 和 自动化功能测试是有意义的。

下面是一些语义化 class 的优势：

## 1. 可读性

下面是一个真实的 HTML 代码片段 使用了原子 class：

	<div class="pb3 pb4-ns pt4 pt5-ns mt4 black-70 fl-l w-50-l">
	  <h1 class="f4 fw6 f1-ns lh-title measure mt0">Heading</h1>
	  <p class="f5 f4-ns fw4 b measure dib-m lh-copy">Tagline</p>
	</div>

注意：

- 阅读单词比阅读缩写更容易.
- 缩写需要被分解并对应认知，假设是我们知道它们的意思。
- 阅读一群 class 名称也很困难。所以 CSS 才有语法。
- 我们需要检查很多 class 才能知道到底发生了什么；哪个 class 覆盖了哪个；哪些用在了一些断点上（响应式）等等。
- 这些 class 看起来模棱两可。例如， `black-70` 指的是颜色还是背景？如果我们需要用检查工具来区分，那么这样的 class 名称是不可读的。
- 内容会被环绕的 HTML 混淆。

下面是同样的代码用了语义化的 class：

	<div class="hero">
	  <h1 class="hero-title">Heading</h1>
	  <p class="hero-tagline">Tagline</p>
	</div>

注意：

- 这些 class 很人容易阅读。没有 mental mapping 的必要。
- 内容不再混淆。
- 我们知道模块从哪开始与结束。
- HTML 少了一半。
- 容易阅读 CSS （用审查工具或在文件中），因为它有一个为此存在的专门语言结构。

## 2. 因为它更容易用来构建响应式网站

想象一个两列的响应式栅格：

* 每列有 `20px` and `50px` padding 在小或大屏幕；
* 每列有 `2em` and `3em` font-size 在小或大屏幕;
* 列堆叠 在小屏幕. 注意 *column* 是一个误导性的 class 名称。

下面是一个典型的使用 视觉和 实用 class 名称的例子：

	<div class="grid clearfix">
	  <div class="col pd20 pd50 fs2 fs3">Column 1</div>
	  <div class="col pd20 pd50 fs2 fs3">Column 2</div>
	</div>

注意：

- 有 7 个 class，一些还会相互覆盖。
- 为了实现列的响应式，我们需要一个 `fs3large` class 等等。 这就是使用了一个命名约定来再现了 CSS 的语言结构。
- 在某些断点，这样的 class 名称有点误导和冗余。 例如 `.clearfix` 并不需要在小屏幕下清除。

我们几乎还没对这个简单的组件进行评估就已经明显的感觉到痛苦了。

下面的同样的代码但是使用了语义化的 class：

	<div class="thing">
	  <div class="thing-thingA"></div>
	  <div class="thing-thingB"></div>
	</div>

注意：

- 这些 class 封装到模块的设计和内容中。
- 调整元素的样式很简单，不需要写多个 class，也不需要改变 HTML。
- 这些 class 在小或大屏幕下都是有意义的。
- 我们可以使用 media query，只作用于我们需要的元素。

> 问题： 一个响应式栅格系统有多重要？ [布局应该适应内容](http://adamsilver.io/articles/stop-using-device-breakpoints/), 而不是围绕它的其他东西。

## 3. 更容易被找到

查找非语义化的 class 字段会出来许多的结果。而语义化的 class 是独一无二的的，一个搜索字段只有一个结果，这使得它在 HTML 中跟更容易被追踪。

## 4. 降低回归的风险

更新一个 视觉 class 会导致跨多元素的回归。更新一个语义化 class 只应用于某个模块，彻底消除了回归。

## 5. 视觉 class 不值得

在某些方面，我们还会使用内联样式。 这更加明确，并消除了 CSS 的痕迹。 内联CSS是有问题的, 例如那样我们无法使用媒体查询。 把 CSS 写在 HTML 显得混乱，并且使得 CSS 没法被缓存。

> 问题:  `.red` 是否和 CSS 中的 `color: red` 是一样的抽象概念?

## 6. 为自动化测试提供了钩子

自动化功能测试通过查找元素，与元素交互来工作。包括以下内容：

1. 点击一个链接
2. 查找一个文本框
3. 输入文字
4. 提交表单
5. 一些标准条件的验证

我们无法使用非语义化的 class 来表示特殊的目标元素。为了测试而添加特殊的钩子显然是一种浪费，用户必须先下载这些东西。

## 7. 为 Javascript 提供了钩子

无法使用非语义化的 class 来区分特殊目标元素，使其能通过 Javascript 得到增强。

## 8. 不需要维护

如果我们基于是什么来命名，那么我们就不需要再次更新 HTML。例如 一个标题永远是标题，不管它看起来怎么样。

而使用了 视觉 class，HTML 和 CSS 都需要更新 （假设没有可用的选择器）。

## 9. 更容易调试

审查一个带有多个原子 class 的元素，意味着需要检查许多的选择器。而语义化的 class ，只需要一个，用起来很方便。

## 10. 标准推荐

对使用 class 属性 ，HTML5 规范 在 3.2.5.7 这样表述：

> "[...] authors are encouraged to use values that describe the nature of the content, rather than values that describe the desired presentation of the content."

## 11. 表达状态化样式更简单

思考下面的 HTML：

	<a class="padding-left-20 red" href="#"></a>

hover 状态下改变 padding 和颜色是一个困难的任务。最好避免类似这样由内部引发的问题。

## 12. 生成了 HTML 更小

正如我们所看到的，原子使得 HTML 膨胀臃肿。语义化的 class 产生更小的 HTML。虽然 CSS 大小可能会增加，但它是可缓存的。

## 结语

语义化 class 是 *MaintainableCSS* 的垫脚石。没有它，其他部分带来的意义也不大。 所以根据它是什么来命名，然后其他都会水到渠成。
