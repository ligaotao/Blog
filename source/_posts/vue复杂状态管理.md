---
title: vue复杂状态管理
date: 2017-09-22 11:47:35
tags:
categories: javascript
---

## 应用场景

当组件的层级比较复杂，且数据来源是唯一的时候，如果在通过`bus`或者`event`就会变的使代码难以理解，
这时我们就可以尝试使用一下`Vuex`来解决这个问题

## 什么是`Vuex`

这里引用一下官方的解释

> Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

也就是说如果有了`Vuex`我们就可以有条理的对这些数据状态进行管理。一个`Vuex`包含：

- state  驱动应用的数据源
- action  应在view上的用户输入导致的状态变化
- view 以声明方式将state映射到视图

我们用一个图来表示一下

![image](/images/vuex.png)