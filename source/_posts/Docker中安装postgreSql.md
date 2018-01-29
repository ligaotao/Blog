---
title: Docker中安装postgreSql
date: 2018-01-29 10:52:11
tags:
categories: Docker
---

- 创建 postgres 帐号

    > postgres Docker 映像中使用的用户和组的 id 都是 999

  `sudo adduser --uid 999 --gid 999 postgres`

  或者使用以下命令

  ``` bash
  sudo adduser postgres
  sudo usermod -u 999 postgres
  sudo groupmod -g 999 postgres
  ```

- 切换到postgres账号

  `sudo su - postgres`

- 获取 PostgreSQL 映像

  `docker pull postgres`

- 创建目录并设置权限, 这里是在登陆postgres之后，只需要在`home/postgres`目录下创建data的文件夹, 切忌这里不能用sudo提升权限

 `mkdir data`

- 在home下创建docker-compose.yml文件：
``` yml
version: "3.0"
services:
  db:
    image: postgres
    restart: always
    ports:
      - "5432:5432"
    volumes:
      - /home/postgres/data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: Hpst1231
```
- 退出postgres账号，使用user账号(管理员账号)，将postgres账号添加到用户组中

`sudo usermod -aG docker postgres`

- 然后再切换到oracle账号，启动服务

`docker-compose up`

- 如果启动正常的话， 可加参数 -d 让docker在后台运行

  `docker-compose up -d`