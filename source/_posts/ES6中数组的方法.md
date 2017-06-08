---
title: ES6中数组的方法
date: 2017-02-02 19:02:42
tags:
---

## from

> from方法可以将两类对象转为数组，一种是类数组对象(array-like-object)，一种是可遍历(iterable)的对象(包括ES6的新增的数据结构set和Map)。

### 类数组转数组

``` javascript
let list = document.querySelectorAll('ul.fancy li')

Array.from(list).forEach(function(li){
  document.write(li)
})
```

上述代码中，`querySelectorAll`方法返回的是一个类似数组的对象，只有将这个对象转为真正的数组，才能使用`forEach`方法。

任何有`length`的对象都可以通过`Array.from`方法转为数组

``` javascript
let obj = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
}
let arr = Array.from(obj)
// [a, b, c]

```
### `from`接受参数

`Array.from`可以接受第二个参数，作用类似于数组的`map`的方法，用来对每个元素进行处理。

```javascript
let arr = [0, 1, 2, 4]
let arrnew = Array.from(arr, x => x*x)
console.log(arrnew)
// 等同于
let arrnew = arr.map(x => x*x)
```

### 字符串转数组

`Array.from`将字符串转为数组，返回字符串长度。这样可以避免`javascript`将大于`\uFFFF`的`Unicode`字符，算作两个字符的`bug`

```javascript
function countSymbols (string) {
  return Array.from(string).length
}
```

## of方法

> `of`方法用于将一组值，转为数组

```javascript
Array.of(3, 11, 8) // [3, 11, 8]
Array.of(3)// [3]
```

## find方法

> `find`方法,用于找出第一个符合条件的数组成员，它的参数是一个回掉函数，找出一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的则返回undefined

```javascript
let array = [1, 2, -3, 4].find(n => n < 0)
console.log(array) // -5
```

`find`回掉函数接受三个参数，分别为`当前的值`、`当前的位置`、`原数组`

### findIndex方法

> 用法于`find`方法类似，返回第一个符合条件的数组成员的位置，没有找到的话返回-1.

```javascript
let index = [1, 5, 11, 16].findIndex(function(value, index, arr) {
  return value > 9
})
console.log(index)
```

`find`与`findIndex`都可以借助`Object.is`方法做到发现数组中的`NaN`,而`indexOf`发现不了。

``` javascript
[NaN].indexOf(NaN) // -1
[NaN].findIndex(y => Object.is(NaN, y)) // 0
```

## fill方法

> `fill()`使用一个值来填充一个数组。

``` javascript
let arr = ['a', 'b', 'c'].fill(7)
// [7, 7, 7]
let arrNew = new Array(3).fill(7)
// [7, 7, 7]
```

上述代码表明，`fill`方法用于空数组的初始化非常方便。数组中已有元素会被全部抹去。
`fill`还可以接受第二和第三个参数，用于指定填充的起始位置和结束位置

``` javascript
let newArr = ['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```
