---
title: RxJS基础
date: 2017-02-04 18:09:36
tags: RxJS
---

## RxJS基础

### 创建流

> Observable.create、of、from、fromEvent( target,eventType )、fromPromise、bindCallback( 把callback写法转换为链式写法 )

```javascript
let exists = Rx.Observable.bindCallback(fs.exists);
exists('file.txt').subscribe( exist=>console.log(`exist? : ${exist} `) )
```

### 事件流

> filter、delay( 延时 )、throttleTime( 时间间隔 )、debounceTime( 事件暂停x毫秒后 )、take( 执行x次后停止 )、takeUtil( 取消订阅 )

```javascript
let inputStream = Rx.Observable.fromEvent(document.querySelector('input'), 'keyup')
let stopStream = Rx.Observable.fromEvent(document.querySelector('button'), 'click')
inputStream.throttleTime(200) // 每隔200毫秒才释放一次
  .takeUtil(stopStream) // 当触发时，停止订阅
  .subscribe(($event)=> {console.log(`${$event.target.value}`)}) // 事件对象
```

### 转换流、过滤流

> map、distinct( 过滤重复 )、distince( 过滤连续重复 )

```javascript
// 输入hello world
input.pluck('target', 'value').distinctUntilChanged()
  .subscribe(value => console.log(value)); // "helo wrd"
input.pluck('target', 'value').distinct()
  .subscribe(value => console.log(value)); // "helo world"
```
