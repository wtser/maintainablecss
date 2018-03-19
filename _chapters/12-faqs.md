---
layout: chapter
title: 问与答
section: Extras
permalink: /chapters/faqs/
description: 关于 MaintainableCSS 的问题和答案
---

如果你无法找到答案，请[在 Github 上提交 issue](https://github.com/adamsilver/maintainablecss.com/issues/new)。谢谢！

## 我可以翻译你的书吗?

是得，这样做：

1. [复刻这个仓库](https://github.com/adamsilver/maintainablecss.com/).
2. 将你的域名指向它
3. 引用来源并让我知道 :)

<!-- ## When should I use this?

If you like to keep things truly simple, use this approach. It works well if you're building long-lived, bespokely designed, responsive sites that scale and evolve over time. -->

## 关于标题等等元素的继承怎么做？

理想情况下，我们的语义HTML与视觉设计的完整性相匹配。这意味着我们希望 所有的 `h1`s 都是一样的。在这种情况下，我们可以声明以下 CSS:

	h1 {
      /* etc */
	}

但是，在大型商业网站中，这种情况真的太少了。在这种情况下，我们应该将样式封装到模块中：

	.module-heading {
	  font-size: ...;
	  color: ...;
	}

<!--## Where do I put media queries?

The screen should adapt to the content, not the other way around.

This means a module's breakpoints shouldn't be predetermined by *small*, *medium* and *large*. Doing this constrains the design and degrades the user experience.

Therefore, all styles&mdash;even those that are wrapped in media queries&mdash;should be located next to regular styles:

	.basket {}

	@media(min-width: 500px) {
      .basket {}
	}

	@media(min-width: 1000px) {
	  .basket {}
	}

	.basket-heading {}

## Where do I put modifiers and states?

States and modifiers, similarly to media queries, should be located in close proximity to the element they pertain to:

	.basket {}

	.basket-isHidden {}

	.basket-heading {}

	.basket-heading--someModifier {}-->

## 无法找到答案？

在[Github](https://github.com/adamsilver/maintainablecss.com/issues/new)提交 issue，我会尽快回复你。谢谢！
