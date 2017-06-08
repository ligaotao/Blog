---
title: javascript类型
date: 2017-01-02 22:36:41
tags: 你不知道的javascript
---

# 类型

>  javascript类型定义：ECMAScript语言中所有值都有一个对应的类型。ECMAScript语言类型包括Undefined、Null、Boolean、String、Number、Object。

## 内置类型

javascript有七种内置类型：

- 空值 (null)
- 未定义 (undefined)
- 布尔值 (boolean)
- 数字 (number)
- 字符串 (string)
- 对象 (object)
- 符号 (symbol, ES6中新增)

我们可以使用`typeof`来查看值的类型，它返回的是类型的字符串。有意思的是这其中类型和他们的字符串值并不是一一对应：

```javascript
typeof undefined === 'undefined' // true
typeof true === 'boolean' // true
typeof 42 === 'number' // true
typeof '42' === 'string' // true
typeof {life: 42} === 'object' // true

// ES6中新增的类型
typeof Symbol() === 'symbol' // true

```

null值的类型不在这里，typeof对它的处理有问题

```javascript
typeof null === 'object' // true
```

判断是否为空需要用到复合条件

```javascript
var a = null
(!a && typeof a === 'object') // true
// 因为null是假值

```

## 小结

在`javascript`中`undefined`与`undeclared`不是一回事，`undefined`是值的一种，而`undeclared`是指的变量还没有声明过。

当试图访问`undefined`的变量时会报错`ReferenceError a is not defined`, 并且typeof 对`undefined`和`undeclared`变量都会返回 `undefined`

然而，可以使用`typeof`的安全机制(阻止报错)来检查`undeclared`变量也是个不错的办法
