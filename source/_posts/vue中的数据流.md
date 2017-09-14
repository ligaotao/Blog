---
title: vue中的Props和事件
date: 2017-09-14 09:46:21
tags:
categories: javascript
---
<script src="https://cdn.bootcss.com/vue/2.4.2/vue.js"></script>

<div id="app">
  <input v-model="content"> <button @click="add">增加任务</button>
  <todo :lists="todos" @remove="remove"></todo>
</div>

<script>
  Vue.component('todo', {
    template: '<ul><li v-for="(list, index) in lists">${list.content} <button @click="remove(index)">x</button></li></ul>',
    delimiters: ['${', '}'],
    props: {
      lists: {
        type: Array,
        default: []
      }
    },
    data () {
      return {
        randomColor: '#fff'
      }
    },
    methods: {
      remove: function(index) {
        this.$emit('remove', index)
      }
    }
  })
  new Vue({
    el: '#app',
    data: {
      todos: [],
      content: ''
    },
    methods: {
      add: function () {
        this.todos.push({content: this.content})
      },
      remove: function (index) {
        this.todos.splice(index, 1)
      }
    }
  })
</script>

在`Vue`中数据应该但向流动，我们不应该在组件内部修改父组件的数据，即使修改应该通过事件通知父元素来进行修改，即子组件仅负责展示。

一个todolist的功能，的流程大概是

![image](/images/emit-props.png)

```html
<div id="app">
  <input v-model="content"> <button @click="add">增加任务</button>
  <todo :lists="todos" @remove="remove"></todo>
</div>

<script>
  Vue.component('todo', {
    template: '<ul><li v-for="(list, index) in lists">${list.content} <button @click="remove(index)">x</button></li></ul>',
    delimiters: ['${', '}'],
    props: {
      lists: {
        type: Array,
        default: []
      }
    },
    data () {
      return {
        randomColor: '#fff'
      }
    },
    methods: {
      remove: function(index) {
        this.$emit('remove', index)
      }
    }
  })
  new Vue({
    el: '#app',
    data: {
      todos: [],
      content: ''
    },
    methods: {
      add: function () {
        this.todos.push({content: this.content})
      },
      remove: function (index) {
        this.todos.splice(index, 1)
      }
    }
  })
</script>
```

