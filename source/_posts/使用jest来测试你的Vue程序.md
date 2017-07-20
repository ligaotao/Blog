---
title: 使用jest来测试你的Vue程序
date: 2017-07-20 14:58:12
tags:
categories: javascript
---

# 使用jest来测试你的Vue程序

## 安装

1. 全局安装`jest`
```bash
npm install jest -g
```
2. 使用`Babel`

```bash
npm install --save-dev babel-jest
```

3. 使用`typescript`来编写和测试

````shell
npm install --save-dev ts-jest @types/jest
````

4. 配置`package.json`文件
```json
{
  // 这里只有jest部分
    "jest": {
      "moduleNameMapper": {
        "^@(.*)$": "<rootDir>/src$1"
      },
      "transform": {
        "^.+\\.js$": "babel-jest",
        ".*\\.(vue)$": "<rootDir>/node_modules/jest-vue-preprocessor",
        ".(ts|tsx)": "<rootDir>/node_modules/ts-jest/preprocessor.js"
      },
      "testRegex": "(/__tests__/.*|\\.(test|spec))\\.(ts|tsx|js)$",
      "moduleFileExtensions": [
        "js",
        "vue",
        "ts",
        "tsx"
      ]
    }
  //...
}
```

## 使用

### 测试函数

```javascript
// sum.js
export function sum (a, b) {
  return a + b
}
```
我们来编写一个测试文件进行测试

```javascript
// sum.test.js
import {sum} from './sum'
test('测试1+2是不是等于3', () => {
  expect(sum(1, 2)).toBe(3)
})
```

### 组件的测试

```vue
<template>
  <div id="app">
    <div class="lorem-class">some test text</div>
    <button v-on:click="clickHandler('value passed to clickHandler')">Click Me!</button>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data () {
      return {
        msg: 'hello world'
      }
    },
    methods: {
      clickHandler(input) {
        return input + 1;
      }
    }
  }
</script>

<style>
  body {
    color: red;
  }
</style>

```
对组件属性及渲染做测试

```javascript
import Vue from 'vue'
import Hello from './Hello.vue'

const doTest = (Component) => {
  const vm = new Vue({
    el: document.createElement('div'),
    render: h => h(Component)
  })
  const mockFn = jest.fn();
  vm.$children[0].clickHandler = mockFn;

  // check if template HTML compiled properly
  expect(vm.$el).toBeDefined();
  expect(vm.$el.querySelector('.lorem-class').textContent).toEqual('some test text');
  expect(vm.$children[0].msg).toEqual('hello world')
  // check if template calls vue methods
  vm.$el.querySelector('button').click();
  expect(mockFn.mock.calls[0][0]).toBe('value passed to clickHandler')
}
describe('preprocessor', () => {
  it('should process a `.vue` file', () => {
    doTest(Hello);
  })
})

```