---
layout: chapter
title: ID
section: Background
permalink: /chapters/ids/
description: 学习为何使用ID作为样式钩子是有问题的，以及你应该怎么用什么替代
---

从语义化角度来说，我们应该使用ID 当某个事物的实例只有一个。有多个的时候使用 class。

然而， [ID 权重高于 class](http://www.w3.org/TR/css3-selectors/#specificity) ，如果我们想覆盖它的样式可能会有问题。


证明一下这个问题，我们使用 ID 覆盖一个元素的颜色，从*红色*改为*蓝色*。

下面是 HTML：

	<div id="module" class="module-override">

CSS 如下：

	#module {
	  color: red;
	}

	.module-override {
	  color: blue;
	}

元素是红色的尽管class 用了蓝色去覆盖。让我们通过用 class 替换 ID ，来修复这个问题：

	<div class="module module-override">

CSS 如下：

	.module {
	  color: red;
	}

	.module-override {
	  color: blue;
	}

现在，元素是蓝色的。问题解决了。

虽然使用 ID会导致一些问题，我们仍然可以把它用在其他方面。例如，我们需要用它来链接：

- 表单字段的 label
- 页面中的锚点链接
- ARIA 属性帮助使用读屏器的用户

## 结语

在需要启用浏览器特殊行为和辅助技术的时候使用 ID。但是避免将它们用于作为调整样式的钩子。
