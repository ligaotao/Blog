---
title: Django-debug-toolbar调试工具配置
date: 2017-12-28 15:48:00
tags:
categories: Python
---

> `Django Debug Toolbar` 是开发`Django`应用程序时的必备工具，可以输出详细的调试信息，会话信息等，大大方便开发

## 环境

- `python` 3.6
- `Django` 1.11.8
- `django-debug-toolbar` 1.9.1

## 安装

通过`pip`安装

```bash
pip install django-debug-toolbar
```

如果想要安装制定版本,只需要在包名后追加`==`和版本号, 例如：

```
pip install django-debug-toolbar==1.9.0
```

## 配置

在`settings.py`通过配置将这个`Debug`引入我们的项目

### 先决条件  

将`debug-toolbar`加入到`INSTALLED_APPS`

```python
# settings.py
INSTALLED_APPS = [
    ...,
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'debug_toolbar',
    ...
]
```
###  URL配置

在路由文件中配置`debug`插件的路径

```python
# urls.py
from django.conf import settings
from django.conf.urls import include, url

if settings.DEBUG:
    import debug_toolbar
    urlpatterns = [
        url(r'^__debug__/', include(debug_toolbar.urls)),
    ] + urlpatterns
```

### 中间件配置

在`settings.py`中加入该插件的中间件

```python
MIDDLEWARE = [
    # ...
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    # ...
]
```

### INTERNAL_IPS

只有在`INTERNAL_IPS`中存在的`IP`, 调试工具栏才会显示。这里我们将本地`IP`加入

```python
# settings.py
INTERNAL_IPS = ['127.0.0.1']
```

### 最后的一件事

确认`DEBUG`模式是否开启

```python
# settings.py
DEBUG = True
```

## 完结 

这时，刷新我们的浏览器就可以在右上角看到我们可爱的`DEBUG`工具了
