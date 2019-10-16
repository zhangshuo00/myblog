---
title: React笔记（二）-Advanced Guides
date: 2019-10-16 08:37:03
tags:
---
# Context
# HOC
***
# Portals
>Portals提供了一种能让子节点渲染到父组件之外的方式
```js
ReactDOM.createPortal(child,container);
//child 是任何可渲染的React子元素
//container 是一个DOM元素
```
当父组件有`overflow:hidden / z-index`时，需要子组件能够在视觉上跳出容器时使用。

