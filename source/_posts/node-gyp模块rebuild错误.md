---
title: node-gyp模块rebuild错误
date: 2017-09-25 16:07:18
tags:
categories: nodejs
---

安装npm包的时候遇到了这个错误， 就是执行node-gyp rebuild的失败的错误，
经过查询一些相关文档，发现 这个需要使用到python的环境和vs 2015的环境，

官方的依赖描述如下

- Option 1: Install [Visual C++ Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools) using the Default Install option.

- Option 2: Install [Visual Studio 2017](https://www.visualstudio.com/zh-hans/vs/community) (or modify an existing installation) and select Common Tools for Visual C++ during setup. This also works with the free Community and Express for Desktop editions.

- install Python 2.7 (v3.x.x is not supported), and run npm config set python 

最后安装过python2.7版本 和 vs2017 后 再执行npm install 完美成功 没有出现报错