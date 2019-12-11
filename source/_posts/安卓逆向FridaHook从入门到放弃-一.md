---
title: 安卓逆向FridaHook从入门到放弃(一)
date: 2019-12-11 09:42:29
tags:
---

## 教程环境

1. window 7
2. python3.7
3. genymotion


## 环境配置

> 需要安装环境所需的python、adb、Frida、genymotion等

1. 安装`python3.7`, 进入官网：https://www.python.org/   选择Downloads>Windows  下载相应版本
2. 安装`ADB`, 注意`ADB`版本问题  ADB版本一定要一致   比如server是41 那么client也必须是41, 不然会出现版本不一致链接不上的情况
3. 下载使用模拟器 `genymotion`, 进入官网：http://www.genymotion.com/  需要先注册再下载, 下载地址 https://www.genymotion.com/download/
4. 安装`Frida`, 在`cmd`中输入`pip install frida-tools`, 安装成功后进入`python shell`, 输入`import frida` 没有错误说明已经安装成功
5. 下载`frida-server`, https://github.com/frida/frida/releases/download/12.7.25/frida-server-12.7.25-android-x86.xz, 并更名为frida-server.xz待用
6. 模拟器选择Google Pixel3 启动
7. 在命令行中输入以下命令
    ```bash
      adb devices
      adb root
      adb push frida-server.xz /data/local/tmp/
      adb shell "unxz /data/local/tmp/frida-server.xz"
      adb shell "chmod 755 /data/local/tmp/frida-server"
      adb shell  "/data/local/tmp/Frida-server &"
    ```
8. 注意这个命令行不能关闭, 另外打开一个命令行执行`frida-ps -U`, 输出PID, Name既是成功

