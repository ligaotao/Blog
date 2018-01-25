---
title: numpy-函数shape的用法
date: 2017-11-22 16:54:23
tags:
categories: python
---

## shape函数

> shape 函数是numpy包中的函数，它的功能是查看矩阵或者数组的维数

首先我们创建一个3*3的矩阵

```shell
>>> from numpy import *

>>> group = array([[1.0,1.1],[1.0,1.0],[0,0],[0,0.1]])
```

使用`shape`函数

```shell

>>> group.shape

# 输出为(4, 2)
# group.shape[0] 为四行 一维数组的长度
# group.shape[1] 为二列 二位数组的长度
```