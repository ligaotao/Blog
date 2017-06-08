---
title: javascript中的值
date: 2017-01-03 23:07:31
tags: 你不知道的javascript
---

# 值

## 整数检测

要检测一个值是否是整数，可以使用ES6的方法`Number.isInteger(..)`方法

``` javascript
Number.isInteger(42) // true
Number.isInteger(42.000) // true
Number.isInteger(42.3) // false

// ES6之前的ployfill

if(!Number.isInteger) {
  Number.isInteger = function (num) {
    return typeof num === 'number' && num % 1 == 0
  }
}
```

## 不是数字的数字

`NaN`是一个特殊值，它和自身不等，是唯一一个非自反的值(自反即 x === x 不成立的值), 而`NaN != NaN`为`true`

如何判断一个值是不是`NaN`,isNaN(..)有严重的缺陷

```javascript
var a = 2 / 'foo'
var b = 'foo'

window.isNaN(a) // true
window.isNaN(b) // true
```

`ES6`可以使用工具函数`Number.isNaN(..)`, 在`ES6`之前的可以

``` javascript
if (!Number.isNaN) {
  Number.isNaN = function (n) {
    return typeof n === 'number' && window.isNaN(n)
  }
}

// 也可以 利用它与自身不等的特性

if (!Number.isNaN) {
  Number.isNaN = function (n) {
    return n !== n
  }
}
```
