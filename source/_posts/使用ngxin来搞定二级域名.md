---
title: 使用ngxin来搞定二级域名
date: 2017-07-25 17:46:42
updated: 2017-09-12 10:20:00
tags:
---

## 需求

通过不同二级域名 均指向服务器的80端口 通过不同前缀来实现访问不同的项目

## 解决方案

ngxin有个配置可以解决这个问题，通过路径来匹配路由指向到不同的项目目录。

```conf
server {
        listen       80;
        server_name  api.ligaotao.cn;
        location / {
            proxy_pass http://127.0.0.1:3000/;
        }
	}
	server {
	listen       80;
	server_name  manager.ligaotao.cn;

	location / {
		root  C:\web\manager;
		index  index.html index.htm;
		try_files $uri $uri/ /index.html;
	}
```