---
layout: chapter
title: 修饰器
section: Core
permalink: /chapters/modifiers/
description: 根据细微的差别使用修饰词来改变外观
---

和状态一样，修饰器也会覆盖样式。当组件（模块）有小的不同的或容易理解的差异时，它们很有用。

以电子商务网站为例，每个类别在标题中都有一个独特的背景图像。 所有的头部有一样的 padding， margin 等。 唯一不同是背景图片。

男士分类下会有一个修饰器：

	<div class="categoryHeader categoryHeader--boys">

类似的，女士分类下会有一个*girls* 修饰器：

	<div class="categoryHeader categoryHeader--girls">

CSS如下：

	.categoryHeader {
	  padding-top: 50px;
	  padding-bottom: 50px;
	  /* etc */
	}

	.categoryHeader--boys {
	  background-image: url(/path/to/boys.jpg);
	}

	.categoryHeader--girls {
	  background-image: url(/path/to/girls.jpg);
	}

差异很小而且很容易理解，这类的复用是更容易维护的。

我们可以给按钮使用相同的方法。大多数的网站有个主要按钮和次要按钮的样式。如果所有这些改变只是一或两种样式，我们可以对主按钮和辅助按钮做一个修饰器：

	.button {
	  padding: 20px;
	  border-radius: 3px;
	  /* etc */
	}

	.button--primary {
	  background-color: green;
	}

	.button--secondary {
	  background-color: #eee;
	}

同样的，这只在区别小并且容易理解的情况下好用。

## 结语

对跨容易理解元素的样式复用，修饰器是一个好的方法。但是，修饰器本身应该被调整。如果它包含了太多覆盖，那么这不是它本来的用途。这时候你应该使用[模块](/chapters/modules/).
