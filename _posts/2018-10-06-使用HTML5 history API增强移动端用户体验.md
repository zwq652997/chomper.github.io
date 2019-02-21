---
layout: post
title: 使用HTML5 history API增强移动端用户体验
date: 2018-10-06
categories: test
tags: 交互体验
---

一般移动端会对 WebView 做一些默认的设置，比如 Hook 用户触摸后退按钮，调用 WebView 后退方法。既然如此，就可以利用这一点，通过操纵浏览记录使用户触摸后退关闭浏览层。

### history

想要操纵浏览记录，就不得不提 **history** 对象了。通过常用的 **back()**、**forward()**、**go()** 方法就可以自由的控制浏览器跳转到任意一个历史记录。
而在 HTML5 中，history 又添加一些新的成员，允许你对浏览记录进行添加和修改却不会刷新页面，这就是解决问题的关键了。

*   **history.pushState(stateObj, title, url)** 用于创建新历史记录；
*   **history.replaceState(stateObj, title, url)** 用于修改当前历史记录；
*   **history.state** 读取当前状态，创建历史记录时会添加状态对象；
*   **window.onpopstate** 是一个事件，当历史记录被修改时会触发。


###简单实现


```javascript

```

就把这个 div 看作一个图片浏览层吧，样式脑补。

```javascript

```

执行history.pushState()时不会触发window.onpopstate，只有前进forward()、后退back()时才会触发，所以在之后还需要调用显示的方法。
对于不支持history.pushState的浏览器执行的还是原来的显示和隐藏方法，handleShow和handleHide在判断内才被重新赋值。
通过在window.onpopstate判断history.state来执行不同的操作，当然你也可以判断location。

以上代码未经测试，只作思路展示，注释说明了一切。

###应用场景

在 SPA 场景中，history 早已大显神通。与history.state相似的还有location.hash，也有其对应的事件window.onhashchange，一般用于处理 IE 低版本的兼容。
抛开本篇描述的功能需求，类似的场景也可以运用。比如左侧导航在原生APP都是可以通过触摸返回来关闭，在浏览器中也可以模拟这种操作体验。
