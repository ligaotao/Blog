---
title: nativescript环境搭建
date: 2018-01-04 15:58:35
tags: nativescript
categories: javascript
---

## 模拟器安装

当安装好`Visual Studio Emulator for Android `后，在命令行内输入

```bash
tns run android
```

后提示找不到设备

最后经过多方面，需要先链接到这个设备的IP

```bash
adb connect 192.168.146.128
tns run android
```

则正常启动