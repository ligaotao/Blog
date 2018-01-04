---
title: Django-JET主题使用
date: 2018-01-03 16:57:35
tags:
categories: Python
thumbnail: /images/django-jet.png
---

# 自定义Dashboard

1. 创建一个`dashboard.py`文件，这里是将该文件放到了项目根目录，并写入如下内容

    ```python
    from django.utils.translation import ugettext_lazy as _
    from jet.dashboard import modules
    from jet.dashboard.dashboard import Dashboard, AppIndexDashboard


    class CustomIndexDashboard(Dashboard):
        columns = 3

        def init_with_context(self, context):
            self.available_children.append(modules.LinkList)
            self.children.append(modules.LinkList(
                _('Support'),
                children=[
                    {
                        'title': _('Django documentation'),
                        'url': 'http://docs.djangoproject.com/',
                        'external': True,
                    },
                    {
                        'title': _('Django "django-users" mailing list'),
                        'url': 'http://groups.google.com/group/django-users',
                        'external': True,
                    },
                    {
                        'title': _('Django irc channel'),
                        'url': 'irc://irc.freenode.net/django',
                        'external': True,
                    },
                ],
                column=0,
                order=0
            ))
    ```

2. 然后在`settings.py`中添加

    ``` python
    JET_INDEX_DASHBOARD = 'dashboard.CustomIndexDashboard'

    ```

3. 这时我们就完成了第一个小`widget`,`LinkList`, 现在页面看起来是这样的

    ![img](/images/jet-link.png)


# Dashboard模块

## LinkList

> class jet.dashboard.modules.LinkList(title=None, children=[], **kwargs)

![img](/images/jet-link.png)

栗子：

``` python
from django.utils.translation import ugettext_lazy as _
from jet.dashboard import modules
from jet.dashboard.dashboard import Dashboard, AppIndexDashboard


class CustomIndexDashboard(Dashboard):
    columns = 3

    def init_with_context(self, context):
        self.available_children.append(modules.LinkList)
        self.children.append(modules.LinkList(
            _('Support'),
            children=[
                {
                    'title': _('Django documentation'),
                    'url': 'http://docs.djangoproject.com/',
                    'external': True,
                },
                {
                    'title': _('Django "django-users" mailing list'),
                    'url': 'http://groups.google.com/group/django-users',
                    'external': True,
                },
                {
                    'title': _('Django irc channel'),
                    'url': 'irc://irc.freenode.net/django',
                    'external': True,
                },
            ],
            column=0,
            order=0
        ))
```

参数有以下几种

### children = []

每一个链接都是一个字典类型，比如：

```python
[
     {
         'title': _('Django documentation'),
         'url': 'http://docs.djangoproject.com/',
         'external': True,
     },
     ...
]
```

### layout = 'stacked'

布局方式，有两种值：`stacked`、`inline`

## AppList

显示每个`App`及应用下`Model`的链接,

### exclude

指定不显示的Model，格式为`App.model`的元组，可以用*代替全部的model，比如`业绩.*`

### models

指定显示的Model，格式为`App.model`的元组，可以用*代替全部的model，比如`业绩.*`

### 栗子

```python
from django.utils.translation import ugettext_lazy as _
from jet.dashboard import modules
from jet.dashboard.dashboard import Dashboard, AppIndexDashboard


class CustomIndexDashboard(Dashboard):
    columns = 3

    def init_with_context(self, context):
        self.children.append(modules.AppList(
            _('应用'),
            exclude=('auth.*', '业绩.个人明细表'),
            models=('业绩.*',),
            column=1,
            order=0
        ))
```

## ModelList

同 AppList


## 历史记录

> 展示管理员 最近的操作记录

### exclude_list

不显示哪些Model的记录, 格式为`App.model`的元组，可以用*代替全部的model，比如`业绩.*`

### include_list

显示哪些Model的记录, 格式为`App.model`的元组，可以用*代替全部的model，比如`业绩.*`

### limit

显示的条数

### 栗子

```python
from django.utils.translation import ugettext_lazy as _
from jet.dashboard import modules
from jet.dashboard.dashboard import Dashboard, AppIndexDashboard


class CustomIndexDashboard(Dashboard):
    columns = 3

    def init_with_context(self, context):
        self.children.append(modules.RecentActions(
            _('操作日志'),
            10,
            exclude_list=('auth.*',),
            include_list=('考核.*',),
            column=2,
            order=0
        ))
```

