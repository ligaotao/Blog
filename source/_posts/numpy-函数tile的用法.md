---
title: numpy-函数tile的用法
date: 2017-11-22 17:14:43
tags:
categories: python
---

## tile函数

函数形式为: tile(A, rep)

功能为重复A的各个维度

参数类型:
- A的类型 array, list, tuple, dict, matrix以及基本数据类型int, string, float以及bool类型
- rep类型 tuple，list, dict, array, int, bool.但不可以是float, string, matrix类型


## tile演示

``` python
from numpy import *

tile(4, (2, 1))
# array([[4], [4]])

tile([4, 2], (2, 5))

# array([[4, 2, 4, 2, 4, 2, 4, 2, 4, 2], [4, 2, 4, 2, 4, 2, 4, 2, 4, 2]])
```