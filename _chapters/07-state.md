---
layout: chapter
title: 状态
section: Core
permalink: /chapters/state/
description: 学习如何基于状态提供模块和组件不同的样式，例如显示，因此和载入状态。
---

经常的，尤其是那些重用户交互的，需要正对元素的状态应用样式。例如，我们需要不同的样式当一个模块（组件）是下面的状态：

- 显示或隐藏
- 激活或未激活
- 禁用或启用
- 载入中或已载入
- 有产品或没有产品
- 是空或者是满

为了表示状态，我们需要一个额外的类，它应该被添加到它所属的模块(或组件)元素中。例如，如果我们的购物车模块需要一个灰色背景当它空的时候，HTML应该这样：

	<div class="basket basket-isEmpty">

CSS 应该这样：

	.basket-isEmpty {
      background-color: #eee;
	}

class 名称带模块（或组件）的前缀因为状态可能是常见的，但是样式却不一定是。例如，空购物车会有一个灰色的背景，但是一个空的搜索框可能有一个绝对定位的图片。

## 状态复用？

有时候，我们可能虚伪能跨组件或模块来复用状态。例如切换元素的可见性。详细讨论见章节 [Javascript](/chapters/javascript/).

## ARIA 属性？

不是所有的视觉状态可以被 [ARIA attribute](https://www.w3.org/TR/wai-aria/states_and_properties#attrs_widgets)表达。例如，没有属性表达 `有产品`。因此，我们应该在需要的时候使用它们，并且添加到 class 。

当然，属性选择器相比受到的[支持更少](https://www.impressivewebs.com/attribute-selectors/). 虽然开发人员可能认为这些浏览器陈旧、不安全或不相关，但我们应该避免使用可能会排斥用户的技术。

## 链式 classes？

我们可以使用链式选择器来表示状态。例如 `.module.isDisabled`。问题是支持的浏览器相比要更少。 我们应该避免不必要地排斥用户的模式，除非有令人信服的理由这样做。

## 结语

如果一个元素的样式需要根据它的状态进行更改，那么我们应该添加一个额外的类来应用这些差异。必要时，使用ARIA属性作为辅助技术，而不是用于样式化。在这样做的过程中，我们采用了一致和包容的方式来设计样式。
