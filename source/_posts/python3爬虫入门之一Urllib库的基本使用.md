---
title: python3爬虫入门之一Urllib库的基本使用
date: 2017-09-11 15:22:53
updated: 2017-09-12 10:20:00
tags:
categories: python
---

## 准备

`python`为`3.6`的版本

## 1.我们先偷偷的爬一下百度

页面是由`HTML`+`CSS`+`JavaScript`组成，HTML是页面骨架内容所在，CSS是页面的装饰所在，JavaScript是负责页面交互的，
我们爬虫是为了获取页面内容的，重点就是获取HTML里的文字内容。

```python
import urllib.request

response = urllib.request.urlopen('http://www.baidu.com')
print(response.read())
```

把代码保存到demo.py, 在命令行运行`python demo.py`我们就能看到结果

![](/images/urllib_01.png)

## 2.urllib.request方法

`urllib.request.urlopen(url, data, timeout)`

1. `url`是请求地址
2. `data`是要发往服务端的数据，默认为`None`
3. `timeout`是超市时间，默认为全局设置的超时时间

## 3.Request构造方法

Request方法的参数

` urllib.request.Request（url，data = None，headers = {}，origin_req_host = None，unverifiable = False，method = None ）`



```python
import urllib.request

request = urllib.request.Request('http://www.baidu.com')
response = urllib.request.urlopen(request)
print(response.read())
```

## GET和POST方式传参

```python
from urllib import request, parse

data = {}
data['wd'] = 'PHP是世界上最美好的语言'
data = parse.urlencode(data)  # 对对象进行url编码
data = data.encode('utf-8')  # 然后进行utf8编码 不然会抱错
response = request.urlopen('https://cn.bing.com/search', data)

print(response.read().decode('utf-8'))  # 解码并打印HTML内容
```

像其他都是类似的，比如发一个`PUT`请求

```python
import urllib.request
DATA = b'some data'
req = urllib.request.Request(url='http://localhost:8080', data=DATA,method='PUT')
with urllib.request.urlopen(req) as f:
    pass
print(f.status)
print(f.reason)
```