---
title: Django下celery异步任务的使用
date: 2019-03-07 11:11:01
tags:
categories: Django
---


## 部署出现的问题

1. 调用官方的例子时出现了`delay not enough values to unpack`这个错误，是由于`win10`上运行`celery4.x`会出现这个问题，解决办法如下。

  ```bash
    # 安装一下eventlet
    pip install eventlet
    # 启动的时候增加参数, 然后就可以正常调用了
    celery -A <mymodule> worker -l info -P eventlet
  ```