---
title: Django入门
date: 2017-12-26 10:15:46
tags:
categories: Python
---

> 本文是基于`Window 10` `Django 2.0` `Python 3.6`的环境写成


## 创建项目

1. 跳转到我们的项目目录，通过执行`django-admin`命令来生成项目

    ```bash
    cd Python
    django-admin startproject Demo
    ```

    如果`django-admin`不工作的话 请查看[帮助](https://docs.djangoproject.com/en/2.0/faq/troubleshooting/#troubleshooting-django-admin)

2. 运行命令后 会创建一些文件及文件夹目录如下

    ``` python
    Demo/
        manage.py
        Demo/
            __init__.py
            settings.py  # Django的配置文件
            urls.py # 路由配置
            wsgi.py
    ```

## 开发服务

是时候见证奇迹了

```bash
python manage.py runserver
```

然后会输出下面的信息

``` bash
Performing system checks...

System check identified no issues (0 silenced).

You have 14 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
December 26, 2017 - 11:49:18
Django version 2.0, using settings 'Demo.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

现在在浏览器里打开`http://127.0.0.1:8000/`就能看到了

如果想要更改启动端口

``` bash
python manage.py runserver 8080
```

如果想更改ip,能够让局域网内的其他用户访问到

```bash
python manage.py runserver 0:8000
```

还需要在`settings.py`中设置允许的`ip`

```python
# settings.py
ALLOWED_HOSTS = ['192.168.1.153']
```

这时我们再通过`http://192.168.1.153:8000`即可访问


## 创建一个App

```
python manage.py startapp polls
```

这样将会创建一个`polls`的文件夹

目录结构如下

``` bash
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

## 编写视图

在`pycharm`或者其他编辑器中打开`/polls/views.py`进行编辑

```python
# polls/views.py

from django.http import HttpResponse


def index(request):
    return HttpResponse("你好！")

```

## 创建路由文件

1. 在`polls`文件夹下创建一个`urls.py`的文件作为我们的路由文件, 并进行编辑

    ```python
    # polls/urls.py
    from django.urls import path

    from . import views

    urlpatterns = [
        path('', views.index, name='index'),
    ] 
    ```
2. 将`polls`下的`urls`导入到`Demo`的路由中

    ```python
    # Demo/urls.py
    from django.urls import include, path
    from django.contrib import admin

    urlpatterns = [
        path('polls/', include('polls.urls')),
        path('admin/', admin.site.urls),
    ]
    ```
3. 现在打开浏览器`http://127.0.0.1:8000/polls/`就能看到

    你好！

4. path 函数的参数: `route`、`view`、`kwargs`、`name`

    - `route`: 一个包含`URL`模式的字符串
    - `view`: `URL`对应的视图函数
    - `kwargs`
    - `name`：`URL`的别名