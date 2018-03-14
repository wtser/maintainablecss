---
layout: chapter
title: 版本
section: Extras
permalink: /chapters/versioning/
description: Learn how MaintainableCSS makes it really easy to upgrade and AB test modules for rapidly evolving websites.
---

我们可能想要对某个模块不同的版本做 A/B 测试，来看哪一个更好。要实现这个，我们需要拷贝该模块并给予一个独一无二的名字。例如，我们想要测试不同的 basket，css 应该像下面这样：

	/* existing module (variant A) */
	.basket {}

	.basket-title {}

	/* new version (variant B) */
	.basket2 {}

	.basket2-title {}

这样在测试期间我们能够维护两个版本直到我们选择了最好的那个。这样做，我们能够很容易的移除多余的模块，因为它们没有耦合在一起。好的代码容易删除。
