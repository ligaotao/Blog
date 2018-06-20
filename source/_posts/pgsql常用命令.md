---
title: pgsql常用命令
date: 2018-06-20 12:26:18
tags:
categories: 数据库
---

## 查询全部数据库

`select datname from pg_database;`

## 创建数据库

`create database ligaotao;`

## 删除数据库

`drop database ligaotao;`

## 连接到数据库

`\c ligaotao`

## 创建表

```
CREATE TABLE DEPARTMENT(
   ID INT PRIMARY KEY      NOT NULL,
   DEPT           CHAR(50) NOT NULL,
   EMP_ID         INT      NOT NULL
);  
```

## 查看表

`\d`

