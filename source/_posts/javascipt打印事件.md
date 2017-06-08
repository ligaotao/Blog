---
title: javascipt打印事件
date: 2017-03-13 23:36:11
tags:
---

## 使用`JavaScript`来检测打印请求

`CSS`有良好支持的机制，当用户打印文档时，才应用某些样式。它们允许您通过设置打印的规则来更改打印机网页的显示方式。这对于常见任务非常有用，例如隐藏非必要内容，使用更多的打印友好排版，以及调整布局以更好地适合纸张的大小和形状。

打印样式表非常适合用于打印的演示更改，但有时需要`JavaScript`来实现某些功能。为了在JavaScript中响应打印请求，您需要浏览器通知您发生了打印请求。

### `onbeforeprint`和`onafterprint`


`ie5+`用户请求打印前和打印后的事件`onbeforeprint`和`onafterprint`事件

```javascript

window.onbeforeprint = function() {
    console.log('在打印之前');
};
window.onafterprint = function() {
    console.log('打印之后');   
};

```

这两个事件不是任何规范的一部分,但是使用起来比较方便。`Firefox`在版本6中添加了这两个事件，但是`WebKit`和`Opera`并不支持这个事件，为了跨浏览器兼容，我们要想其他的方法解决。

## `WebKit`实现方案

`window.matchMedia`API提供了当前`document`的媒体查询的信息。例如：

``` javascript

if (window.matchMedia(' (min-width: 600px) ').matches) {  
    console.log('当前窗口最小为600px');
} else {
    console.log('当前窗口小于600px');
}

```

你还可以监听该API的事件，当发生变化时触发。如果你希望当窗口大于600px时接受到通知，即可使用以下方法：

```javascript
var mediaQueryList = window.matchMedia(' (min-width: 600px) ');
mediaQueryList.addListener(function(mql) {
    if (mql.matches) {
        console.log('当前窗口最小为600px');
    } else {
        console.log('当前窗口小于600px');
    }
})
```

这个方法也可以用来监听`print`

``` javascript
var mediaQueryList = window.matchMedia('print');
mediaQueryList.addListener(function(mql) {
    if (mql.matches) {
        console.log('onbeforeprint')
    } else {
        console.log('onafterprint')
    }
})
```

在`Chrome 9+`和`Safari 5.1`支持的较好，需要注意的是但是，它在`Firefox`或`IE10`不工作，即使他们都支持`window.matchMedia`

## 最后处理

```javascript
(function() {
    var beforePrint = function() {
        console.log('打印前');
    };
    var afterPrint = function() {
        console.log('打印后');
    };

    if (window.matchMedia) {
        var mediaQueryList = window.matchMedia('print');
        mediaQueryList.addListener(function(mql) {
            if (mql.matches) {
                beforePrint();
            } else {
                afterPrint();
            }
        });
    }

    window.onbeforeprint = beforePrint;
    window.onafterprint = afterPrint;
}())
```

注:

1. 虽然可以使用这个来监听打印来更改视图，但是隐藏后的元素也会出于打印的高度之中，会出现，打印预览会多出一页或多页的空白页
