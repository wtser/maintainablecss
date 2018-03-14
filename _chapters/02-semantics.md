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

语义化的 class 不表达它们的样式，不过没关系。那是 CSS 做的事情。语义化 class 对 HTML, CSS, Javascript and 自动化功能测试是有意义的。

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

- These classes are easy to read. No mental mapping is required.
- The content is no longer obfuscated.
- We know where the module begins and ends.
- The HTML is half the size.
- It's easy to read the CSS (in the inspector or in the file) because it has dedicated language constructs that exist for this purpose.

## 2. 因为它更容易用来构建响应式网站

Imagine coding a two-column responsive grid whereby:

* each column has `20px` and `50px` padding on small and large screens;
* each column has `2em` and `3em` font-size on small and large screens; and
* the columns stack on small screens. Note that *column* is now a misleading class name.

Here's how this is typically done using visual and utility classes:

	<div class="grid clearfix">
	  <div class="col pd20 pd50 fs2 fs3">Column 1</div>
	  <div class="col pd20 pd50 fs2 fs3">Column 2</div>
	</div>

Notes:

- There are 7 classes, some of which override each other.
- To make the columns actually responsive we would need a `fs3large` class etc. This means using a naming convention that recreates language constructs found in CSS.
- At certain break points, the classes are misleading and redundant. For example `.clearfix` doesn't clear on small screens.

We've barely evaluated this simple component and yet there is significant pain already.

Here's the same thing using semantic classes:

	<div class="thing">
	  <div class="thing-thingA"></div>
	  <div class="thing-thingB"></div>
	</div>

Notes:

- These classes are encapsulated to the module's design and content.
- It's easy to style elements without having to write a multitude of classes and changing the HTML again.
- These classes are meaningful in small and big screens.
- We can use a media query, to clear elements only when needed.

> Question: How valuable is a codified responsive grid system? A [layout should adapt to the content](http://adamsilver.io/articles/stop-using-device-breakpoints/), not the other way around.

## 3. 更容易被找到

Searching for HTML with a non-semantic class yields many results. As semantic classes are unique, a search yields only one result, making it easy to track down the HTML.

## 4. Because they eliminate the risk of regression

Updating a visual class could cause regression across a multitude of elements. Updating a semantic class only applies to the module in question, eliminating regression altogether.

## 5. Because visual classes aren't worth it

In some respects we may as well inline styles. This is more explicit and reduces the CSS footprint to zero. Inline CSS is a problem though, because we can't use media queries for example. And placing CSS in HTML mixes concerns and removes the ability to cache it.

> Question: Isn't `.red` the exact same abstraction that CSS already gives us for free with `color: red`?

## 6. 为自动化测试提供了钩子

Automated functional tests work by searching for, and interacting with elements. This may include:

1. clicking a link
2. finding a text box
3. typing in text
4. submitting a form
5. verifying some criteria

We can't use non-semantic classes to target specific elements. And adding hooks specifically for tests is wasteful as the user has to download this stuff.

## 7. 为 Javascript 提供了钩子

We can't use non-semantic classes to target specific elements in order to enhance them with Javascript.

## 8. 不需要维护

If we name a thing based on what it is, we won't have to update the HTML again e.g. a heading is always a heading, no matter what it *looks* like.

With visual classes, both the HTML and the CSS need updating (assuming there aren't any selectors available for use).

## 9. 更容易调试

Inspecting an element with a multitude of atomic classes, means wading through many selectors. With a semantic class, there is only one, making it far easier to work with.

## 10. 标准推荐

对使用 class 属性 ，HTML5 规范 在 3.2.5.7 这样表述：

> "[...] authors are encouraged to use values that describe the nature of the content, rather than values that describe the desired presentation of the content."

## 11. 表达状态化样式更简单

思考下面的 HTML：

	<a class="padding-left-20 red" href="#"></a>

hover 状态下改变 padding 和颜色是一个困难的任务。最好避免类似这样由内部引发的问题。

## 12. Because they produce a small HTML footprint

As we've seen above, atomic classes bloat HTML. Semantic classes result in smaller HTML. And whilst the CSS may increase in size, it's cacheable.

## 结语

语义化 class 是 *MaintainableCSS* 的垫脚石。没有它，其他部分带来的意义也不大。 所以根据它是什么来命名，然后其他都会水到渠成。
