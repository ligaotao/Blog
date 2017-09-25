---
title: Redis安装
date: 2017-09-25 15:45:49
tags:
categories: 工具类
---


## Redis的安装

[下载地址](https://github.com/MSOpenTech/redis/releases)

这里是`window`下安装的`Redis`，我们就选择`msi`的安装包进行安装，

为了方便能直接执行`redis`的命令 我们可以把路径加入到系统的环境变量里

然后打开一个`cmd`窗口 运行命令`redis-server.exe redis.windows.conf`

`redis.windows.conf`则可以省略 执行完界面如下:

![image](/images/redis-setup.png)

## 简单的使用

redis目录下运行 redis-cli.exe -h 127.0.0.1 -p 6379 。

设置键值对 set name lee

取出键值对 get name

![image](/images/redis-set.png)