---
title: linux下前端环境搭建
date: 2017-09-29 14:32:16
tags:
categories: Linux
---

## 系统环境

`ubuntu 16 32位`

## git

`sudo apt-get install git`

## nodejs环境的安装

1. 获取nodejs源码
``` bash
$ sudo git clone https://github.com/nodejs/node.git
Cloning into 'node'...
```
2. 修改目录权限
`$ sudo chmod -R 755 node`
3. 使用`./configure`创建编译文件，并按照：
``` bash
$ cd node
$ sudo ./configure
$ sudo make
$ sudo make install
```
4. 查看是否安装成功
```bash
$ node -v
v9.0.0-pre
```


## nginx配置

`apt-get install nginx`

配置文件生成目录为`/etc/nginx`


## mogondb安装

[官方教程](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition)

由于我的系统是32位的不能够这样安装

直接使用了

```bash
sudo apt-get install -y mongodb
```