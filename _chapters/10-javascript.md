---
layout: chapter
title: Javascript
section: Extras
permalink: /chapters/javascript/
description: 如何在编写可维护 CSS 的同时编写可维护的 JS
---

我们可能希望使用 JS 在给多个模块或组件应用相同的行为。

例如，我们使用 `Collapser` 结构来切换元素的可见性。

有两张办法可以实现，在前面的章节中我们都已经提到过。
## 1. 状态封装到模块中

为此，我们需要为构造函数指定一个特定于模块的状态 class:

	var module1Collapser = new Collapser(element1, {
	  cssHideClass: 'moduleA-isHidden'
	});

	var module2Collapser = new Collapser(element2, {
	  cssHideClass: 'moduleB-isHidden'
	});

复用的 CSS 样式如下：

	.moduleA-isHidden,
	.moduleB-isHidden {
      display: none;
	}

需要权衡的是这个列表会快速增长（可以使用 mixin）。并且每次我们添加行为，需要更新 CSS。一个小小的改变，也是一个改变。在这里例子里我们可以考虑添加一个全局的状态 class。

## 2. 创建一个全局状态 class

如果我们发现我们在重复一样的样式给多个模块，最好使用全局状态 class：

	.globalState-isHidden {
      display: none;
	}

这个办法确实让我们远离了长长点的驼峰列表。并且我们也不再需要在实例化的时候区分模块的 class 。因为全局 class 将从内部引用。

	var module1Collapser = new Collapser(element1);
	var module2Collapser = new Collapser(element2);

然而，这个办法并不总是管用，我们可能有两个不同的模块，*行为*一样，但是*表现*不一样，就像我们在[状态](/chapters/state/)章节讨论过的那样。

## 3. 两者结合

我们可以结合这两种方法，把默认的状态 class 放入全局状态 class中。在需要时，我们可以在实例化过程中指定一个类，如上面的第一个示例所示。

## 结语

当我们思考状态，特别是和JS结合时，我们需要考虑这个状态如何影响行为和样式。不同的模块也许共享同样的行为，但看起来不同。 经过仔细考虑，我们可以选择正确的解决方案。

<!-- display: flex vs display: block -->
