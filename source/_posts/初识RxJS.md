---
title: 初识RxJS
date: 2017-02-03 10:59:35
tags:
categories: javascript
---

# RxJS

> `RxJS`是一个解决异步问题的JS开发库.它起源于 `Reactive Extensions` 项目，它带来了观察者模式和函数式编程的相结合的最佳实践。 观察者模式是一个被实践证明的模式，基于生产者（事件的创建者）和消费者（事件的监听者）的逻辑分离关系.

## 为什么选择`RxJS`

为什么要选择`RxJS`?`Promises`是什么?`Promises`适用于解决异步操作，例如`XMLHttpRequest`请求异步行为。`RxJS`统一了`Promises`、回掉、`DOM`输入、`Web Works`等。

## RxJS介绍

> `RxJS`在`ng2`、`redux-observable`的数据层中有重要地位。本文主要介绍六大概念(`Observable`、`Observer`、`subscription`、`Subject`、`Operators`、`Scheduler`).

其他`Api`请关注其他几篇文章:

- `transfrom`(转换)
- `filter`(过滤)
- `combination/multicasting`(组合/广播)
- `ErrorHanding/Condition/Mathematical`(错误处理、情况处理、数学方法)

## 安装

webpack中使用

```javascript
import {Observable} from 'rxjs/Observable' // 按需导入
import 'rxjs/add/observable/merge' // 按需导入merge函数

```

## 概念

- Observable( 可被观察的 ) : 是一个包含来自未来、可以被使用的值( value )或事件( event )的集合
- Observe( 观察者 )：是一个知道如何监听、处理来自Obervable的值的函数集合
- Subscription( 订阅 )：代表着Observable的执行动作，我们可以使用它来停止Obervable继续执行
- Operators( 操作 )：一系列可以操作集合的pure function，像是过滤( filter )、转换( map )等等
- Subject(  )：相当于一个事件发射器，是唯一能够向多个Observer广播值( value )的唯一手段
- Schedulers( 调度 )：是一个中央调度员，帮助我们控制并发，协调计算( setTimeout、requestAnimationFrame等 )

### Observable

通常而言，Observable都会延迟产生值 ，比如当我们subscribe一个observable的时候它才会向我们发送这些值

```javascript
let observable = Rx.Observable.range(1,3)
```
- pull( 拉取 ) 每个函数都是一个数据的生产者，每个调用函数的那个'人'，都会希望从这个函数中能够获得(pull) 唯一的返回值
- push( 推送 ) 在数据生产者中( 如函数 )，会在特定时候把数据推送至消费者，消费者在获得数据之前啥也不会做
- Observable与函数、promsise的对比：函数是当调用才同步计算，并最终只返回一个值的；promise是会或者不会返回一个值；Observable是当调用才同步或者异步地计算，并可能产生0到无穷多个值的。Observable就像一个没有参数的函数，并不断生成一些值供我们使用，因此它也像是一个事件发射机( EventEmitters )。在Observable中subscribe就像call一个函数，你订阅它，它才会被'启动'。同一个Observable对于不同的subscribe，是不会共享结果的( 通常情况下这样子的，但可以通过调用api来共享 )。
- Observable四大核心：创建 、订阅 、 执行 、销毁 。

订阅( subscribe )。当对一个Observable调用多个subscribe函数并创建多个observe时，observe之间不会共享任何东西，因为在Observable.create内部是对observe列表调用各自的回调的

```javascript
Observable.create(function subscribe(observe){...})
```
执行( Executing )。Next函数能够将数据传递给Observer，同时在执行期间，能在Observable内部调用多个Next( )函数。同时建议在Observabl内部使用try/catch语法。

```javascript
// 销毁Observe
let observable = Rx.Observable.from([10, 20, 30])
let subscription = observable.subscribe(x => console.log(x))

// 销毁
subscription.unsubscribe()
```

### Observer(观察者)

> 什么是观察者？观察者其实是数据的消费者，把来自Observble的数据拿过来使用。同时，Observer的本质是一系列的回调函数，是来自于Observable传递数据后的回调函数。我们可以直接通过subscribe函数创建观察者

```javascript
observable.subscribe(
  x => console.log('Observer 得到的下一个之' + x),
  err => console.log('发生错误' + err),
  () => console.log('完成');
)

```
### Subscription(订阅者)

> `Subscription`是`observable`的执行对象，可以通过`unsubscribe`来销毁，同时可以使用`add`来销毁多个。

``` javascript
var subscription = observable1.subscribe(x => console.log('first: ' + x));
var childSubscription = observable2.subscribe(x => console.log('second: ' + x));

subscription.add(childSubscription);

setTimeout(() => {
  subscription.unsubscribe();
}, 1000);

```

### Subject

> 什么是Subject？它是在Rx中一种比较特殊的Observable( 同时它也是Observer )，它能够让值( value )同时向多个Observer传播( 广播 )。而一般的Observable都是' 单播 '形式，即：每一个订阅了同一个Observable的observer，实际上是拥有不同的、独立的Observable的执行( 原文：each subscribed Observer owns an independent execution of the Observable )，而Subject是多播的。

```javascript
// Observable对比Subject
let source = Rx.Observable.create((observer)=>{
    observer.next('1');
    observer.next('2');
});
source.subscribe((x)=>{console.log(x);});
source.subscribe((x)=>{console.log(x);});
// 输出 1 2 1 2
let subject = new Rx.Subject();
subject.subscribe((x)=>{console.log(`${x}`);});
subject.subscribe((x)=>{console.log(`${x}`);});
subject.next(1);
subject.next(2);
// 输出 1 1 2 2
```
