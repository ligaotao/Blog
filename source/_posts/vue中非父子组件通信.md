---
title: vue中非父子组件通信
date: 2017-09-15 11:08:02
tags:
categories: javascript
---

## 介绍

有的时候我们会遇到非父子组件之间需要通信, 用`vuex`又比较重，这时候我们就可以用`bus`来
实现非父子组件通信。即使用一个空的vue实例来负责这个工作。如果比较复杂的逻辑交互，还是去使用`vuex`把


## 示意图

![image](/images/event-bus.png)

``` javascript
var bus = new Vue()

// 触发组件 A 中的事件  --- 组件A
bus.$emit('id-selected', 1)

// 在组件 B 创建的钩子中监听事件 -- 组件B
bus.$on('id-selected', function (id) {
  // ...
})
```

## 实战

还是那之前的`todo`， 我们通过`bus`的方式写一次，这里 我们通过`add`组件 向bus派发一个`add`事件，把我们想添加的任务描述放在参数里;然后在`todo`组件里，在`created`钩子中监听了`bus`的事件， 来执行我们的添加操作，
成功的将内容传入`todo`完成通讯；最终实现效果如下：

<script src="https://cdn.bootcss.com/vue/2.4.2/vue.js"></script>

<div id="app">
  <add></add>
  <todo></todo>
</div>

<script>
  var bus = new Vue()
  Vue.component('add', {
    template: '<div><input v-model="content"> <button @click="add">增加任务</button></div>',
    data: function () {
      return {
        content: ''
      }
    },
    methods: {
      add: function () {
        bus.$emit('add', {content: this.content})
      }
    }
  })

  Vue.component('todo', {
    template: '<ul><li v-for="(list, index) in lists">${list.content} <button @click="remove(index)">x</button></li></ul>',
    delimiters: ['${', '}'],
    data () {
      return {
        lists: []
      }
    },
    created: function () {
      bus.$on('add', this.add)
    },
    methods: {
      add: function (obj) {
        this.lists.push(obj)
      },
      remove: function(index) {
        this.lists.splice(index, 1)
      }
    }
  })
  new Vue({
    el: '#app'
  })
</script>


```javascript
<div id="app">
  <add></add>
  <todo></todo>
</div>

<script>
  var bus = new Vue()
  Vue.component('add', {
    template: '<div><input v-model="content"> <button @click="add">增加任务</button></div>',
    data: function () {
      return {
        content: ''
      }
    },
    methods: {
      add: function () {
        bus.$emit('add', {content: this.content})
      }
    }
  })

  Vue.component('todo', {
    template: '<ul><li v-for="(list, index) in lists">${list.content} <button @click="remove(index)">x</button></li></ul>',
    delimiters: ['${', '}'],
    data () {
      return {
        lists: []
      }
    },
    created: function () {
      bus.$on('add', this.add)
    },
    methods: {
      add: function (obj) {
        this.lists.push(obj)
      },
      remove: function(index) {
        this.lists.splice(index, 1)
      }
    }
  })
  new Vue({
    el: '#app'
  })
</script>
```