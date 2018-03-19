---
layout: chapter
title: 组织
section: Extras
permalink: /chapters/organisation/
description: 学习如何组织你的 CSS 文件。
---

好的代码容易被找到，而容易被找到的代码是因为组织的好。因此，我们希望我们的CSS组织有序。一般来说，有两种方法可供选择，我们将在这一章中讨论。

## 1. CSS 在一个单独的文件夹中

这种方法把所有的 CSS 放在一个文件夹中：

	/path/to/css
	  /vendor
        some3rdParty.css
        someOther3rdParty.css
	  /yourApp
	    some.css
	    global.css
	    basket.css

### 注意

* 第三方 的 CSS 文件位于 `/vendor`.
* 应用的 CSS 位于 `/yourApp` ， *yourApp* 是项目名。
* 这种方法便于部署，因为编译脚本指定一个目标文件夹很容易实现文件打包和压缩。
* 这是最常见的方法但是不意味着是最好的。

## 2. CSS 在模块文件夹中

这种方法将 CSS 按模块放在不同的文件夹中：

	/global
	  /css
	    resetPerhaps.css
	    global.css
        etc.css
	/basket
      /controllers
        ...
      /templates
        basket.html
        emptyBasket.html
      /partials
        basketHeader.html
        basketSummary.html
      /js
        ...
      /css
        basket.css
	/header
	  ...

### 注意

* 一般情况下我们定位自身是通过功能而不是技术，使得这个方法更受欢迎。
* 全局CSS需要一个自己的文件夹，本质上全局样式不属于一个模块。
* 这方法更可能会遇到 *31 CSS 文件限制问题*，下面会讲这个问题。

## 31 个 CSS 文件限制问题

无论什么方法，都要小心这个在IE上的某些版本上会出现的限制。例如 Internet Explorer 9 会忽略第32个（或第33个）的文件。

在生存环境上，这也没问题，我们可以将 CSS 打包降低 HTTP 请求。但是本地的开发环境最好是使用源文件开发这样使得调试更容易。在传统浏览器中，bug 通常会出现。

**如果你有一个编译步骤** 在本地开发环境，就像使用CSS预处理器一样。你就无需担心，这个预处理器会打包所有文件。

**如果你没有编译步骤** 在本地开发环境，因为这样调试源文件更容易，那么你可以用下面两种方法中的一种来补救：

### 1. 添加一个本地化连接 CSS 的选项

这样你可以模拟生产环境，在老旧传统的浏览器中调试CSS。

### 2. 使用少于32个文件

因为你可能有超过31个模块，你无法通过模块来组织。你不得不把几个模块合并在同一个 CSS文件中。

## 结语

在本章中，我们讨论了组织CSS的两种方法。不管用了哪种方法，我们应该小心31个 CSS文件限制问题，因为这使得在最容易引起麻烦的浏览器中调试 CSS 变得更加困难。
