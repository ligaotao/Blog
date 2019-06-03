---
title: docker常用命令
date: 2018-12-21 09:35:09
tags:
---


### 移除无用的容器

在服务器部署的时候经常使用load命令导致有许多无用的容器

`docker rmi -f  `docker images | grep '<none>' | awk '{print $3}'` `