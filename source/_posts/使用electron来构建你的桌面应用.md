---
title: 使用electron来构建你的桌面应用
date: 2017-07-11 16:00:09
tags:
categories: javascript
---

# 使用electron来构建你的桌面应用

> 我们使用了`electron-vue`使用`vue`来开发桌面应用

- 首先，如果我们使用的`npm`不是淘宝源，建议更改成淘宝源，在国内你懂的...

``` shell
  npm config set registry https://registry.npm.taobao.org
```
- 通过`vue-cli`初始化项目

``` shell
npm install -g vue-cli
```

- 初始化项目

``` shell
vue init simulatedgreg/electron-vue my-project
cd my-project
npm install
```

## 构建

> 这里选择的是`electron-packager`进行打包

当打包的时候，需要下载几个zip包，由于网路不好一直超时，下载不下来。
经过查，在[electron](https://github.com/electron/electron/releases)上下载对应的几个平台的zip包，
放到`C:\Users\Administrator\.electron`中即可

所需的文件

- electron-v1.7.4-darwin-x64.zip
- electron-v1.7.4-linux-x64.zip
- electron-v1.7.4-mas-x64.zip
- electron-v1.7.4-win32-x64.zip

然后再执行 `npm run build`即可

生成的目录是 `/build/`