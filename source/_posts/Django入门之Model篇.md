---
title: Django入门之Model篇
date: 2018-01-02 15:08:49
tags:
categories: Django
---

## 创建Models

在我们的`poll`的`App`中，我们将要创建两个`Models`: `Question` 和 `Choice`， 一个`Question`包含一个问题和一个发布日期，一个`Choice`包含两个字段：选择内容和得票统计。每个Choice和一个Question关联。

这些概念可以用`Python`的类来表示, 编辑我们的`polls/models.py`文件

```python
# polls/models.py

from django.db import models


# Create your models here.
class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

每一个模型都有一个类来表示，每个字段通过Field类来表示是什么类型的字段，Field还有一些可选参数，比如`default=0, max_length=200`等，这些参数不仅被用于数据库模式，还在表单验证出使用。


这里还有关系的定义，比如`ForeignKey`，它将告诉`Django`每一个`Choice`都只关联一个`Question`,

`Django`支持常见的数据库关系关联
- 多对一 `ForeignKey`
- 多对多 `ManyToManyField`
- 一对一 `OneToOneField`

## 激活Models

通过上边简洁的代码，`Django`就可以自动完成下面两个工作

1. 为该应用(polls)创建数据库表(CREATE TABLE语句)
2. 为`Question`对象和`Choice`对象创建一个访问数据库的`python API`

首先需要告诉我们的项目，polls已经被安装好，修改`Demo/settings.py`，将polls加入到`INSTALLED_APPS`中

```python
# Demo/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls.apps.PollsConfig',
]
```

## 常见命令

通过这些命令可以对models进行变更

### makemigrations

> makemigrations命令会创建一些迁移文件，迁移是 Django 如何储存模型的变化（以及您的数据库模式），它们只是磁盘上的文件。

让我们运行另外一个命令

```bash
python manage.py makemigrations polls
```

你将会看到下面的内容

```bash
Migrations for 'polls':
  polls/migrations/0001_initial.py:
    - Create model Choice
    - Create model Question
    - Add field question to choice
```

### sqlmigrate

> sqlmigrate命令接收迁移文件的名字并返回它们的SQL语句, 它并不会真的在数据库上运行迁移操作，只是将Sql语句打印出来。

比如：

``` bash
python manage.py sqlmigrate polls 0001
```

就会看到输出的语句

```bash
BEGIN;
--
-- Create model Choice
--
CREATE TABLE "polls_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL);
--
-- Create model Question
--
CREATE TABLE "polls_question" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "question_text" varchar(200) NOT NULL, "pub_date" datetime NOT NUL
L);
--
-- Add field question to choice
--
ALTER TABLE "polls_choice" RENAME TO "polls_choice__old";
CREATE TABLE "polls_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL, "ques
tion_id" integer NOT NULL REFERENCES "polls_question" ("id") DEFERRABLE INITIALLY DEFERRED);
INSERT INTO "polls_choice" ("id", "choice_text", "votes", "question_id") SELECT "id", "choice_text", "votes", NULL FROM "polls_choice__old";
DROP TABLE "polls_choice__old";
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");
COMMIT;

```

### migrate

> migrate命令会找出所有还没有被应用的迁移文件（Django使用数据库中一个叫做django_migrations的特殊表来追踪哪些迁移文件已经被应用过），并且在你的数据库上运行它们 —— 本质上来讲，就是使你的数据库模式和你改动后的模型进行同步。

所以修改模型并实现变更的话有三个步骤：
1. 在`models.py`中修改模型
1. 运行`python manage.py makemigrations` 创建迁移文件
1. 运行`python manage.py migrate` ，将这些改变更新到数据库中。