---
title: 内外网穿透和docker项目部署
date: 2018-06-17 09:59:49
tags:
categories: Linux
---

# 内外网穿透

> 假如我们现在有一台服务器在内网(内网1)机房， 还有一台能够访问内网1和内网2的电脑，内网1和内网2互不相同， 怎么让内网2的其他电脑访问内网1？

## ssh 隧道

1. 由于访问内网1，需要使用指定的ip，我们将电脑1的设置为固定

  ip： 11.190.134.22

  网关: 11.190.134.1

2. 然后将wlan设置为自动获取ip 电脑1通过wifi和其他电脑处于内网2

3. 在电脑1上创建路由链路， 通过管理员运行`cmd`, route add 11.190.0.0/16 11.190.134.1

4. 如果有防火墙 则关闭防火墙

5. 开启隧道 `ssh -L 0.0.0.0:22:127.0.0.1:22 -L 0.0.0.0:5432:127.0.0.1:5432 hpst@11.190.35.201`

6. 其他内网电脑 即可通过电脑1的 wlan分配的ip 192.168.0.113 访问内网机器 11.190.35.201，如：`ssh hpst@192.168.0.100`


# docker项目的离线更新

> 项目属于内网，不能直接在线进行build，只能通过在外网的电脑进行，然后将包导入到内网服务器上

1. 由于阿里云服务器上已经存在 /home/zhangyan/hpjx_docker/ 如果没有则从内网项目上下载 然后传到阿里云上

2. 切换到hpjx_docker/web 执行git pull 拉取最新的代码

3. 在目录hpjx_docker 中执行 `docker-compose build`

4. 压缩存储docker的离线文件 `docker save hpjxdocker_web | gzip > hpjx_web.gz`

5. 将hpjx_web.gz导出的文件上传到内网服务器上

6. 解压hpjx_web.gz `gunzip hpjx_web.gz`

7. 将项目重新载入 `docker load -i [images]` images为 解压出的文件 如 `docker load -i hpjx_web`

8. 跳转到内网的hpjx_docker 中执行 `docker-compose down` 然后再执行 `docker-compose up -d`