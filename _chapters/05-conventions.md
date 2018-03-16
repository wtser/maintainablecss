---
layout: chapter
title: 约定
section: Core
permalink: /chapters/conventions/
description: MaintainableCSS 用于编写模块，组件和状态的简单约定
---

*MaintainableCSS* 有如下约定：

	.<模块>[-<组件>][-<状态>] {}

方括号是可选的，取决于模块。下面是一些例子：

	/* 模块容器 */
	.searchResults {}

	/* 组件 */
	.searchResults-heading {}

	/* 状态 */
	.searchResults-isLoading {}

注意：

- 组件和状态通过中划线分隔
- 命名驼峰写法
- 模块名称作为选择器前缀

## 必须给每个元素一个 class 名称吗？

不是的。你可以写成 `.searchResults p` 。而且有时候你不得不这样做，例如你在使用 markdown。 不过注意如果你嵌套了一个模块也包含了`p`，他会继承样式，可能需要覆盖样式。

## 为为什么必须给模块名称加前缀？

好问题。下面是一个没有前缀的例子：

	<div class="basket">
	  <div class="heading">

CSS 代码：

	/* module */
	.basket {}

	/* heading component of basket module */
	.basket .heading {}

存在两个问题：

1. 看 HTML, 很难区分谁是模块谁是组件
2.  `.basket .heading` 组件会继承 `.heading` 模块的样式，这个模块可能会有意想不到的副作用。
