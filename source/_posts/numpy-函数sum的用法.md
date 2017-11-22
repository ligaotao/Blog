---
title: numpy-函数sum的用法
tags:
categories: python
---

## sum函数

> numpy.sum(a, axis=None, dtype=None, out=None, keepdims=<class numpy._globals._NoValue>)[source]

参数：	
- a：array_like
总和的要素。
- axis：无或int或tuple ints，可选
沿着其执行和的轴或轴。默认值axis = None将对输入数组的所有元素求和。如果轴为负，则从最后一个轴计数到第一个轴。
版本1.7.0中的新功能。
如果axis是ints的元组，则对元组中指定的所有轴执行求和，而不是像以前一样对单个轴或所有轴执行求和。
- dtype：dtype，可选
返回的数组和累加器元素的累加器的类型。除非a具有精度低于默认平台整数的整数dtype，因此默认使用a的dtype。在这种情况下，如果a被签名，则使用平台整数，而如果a是无符号的，则使用与平台整数相同精度的无符号整数。
- out：ndarray，可选
用于放置结果的替代输出数组。它必须具有与预期输出相同的形状，但如果必要，将输出输出值的类型。
- keepdims：bool，可选
如果设置为True，则缩小的轴在结果中保留为尺寸为1的尺寸。使用此选项，结果将相对于原始arr正确广播。
如果传递默认值，则keepdims将不会传递到ndarray的子类的sum如果子类sum方法不实现keepdims，则会引发任何异常。
返回：	
- sum_along_axis：ndarray
与a形状相同的数组，指定的轴已删除。如果a是0-d数组，或者如果轴是无，则返回标量。如果指定输出数组，则返回对out的引用。


## sum演示

``` python
from numpy import *

group = array([[4, 2, 4, 2, 4, 2, 4, 2, 4, 2], [4, 2, 4, 2, 4, 2, 4, 2, 4, 2]])
group.sum(axis=1)
# 相当于将每行求和
# array([30, 30])
group.sum(axis=0)
# 相当于没列求和
# array([8, 4, 8, 4, 8, 4, 8, 4, 8, 4])
```