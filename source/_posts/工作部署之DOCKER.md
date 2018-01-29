
---
title: 工作之Docker部署
date: 2018-01-24 10:59:35
tags:
categories: Docker
---

- 创建 Oracle 帐号

  `sudo adduser --uid 54321 --gid 54321 oracle`

  或者使用以下命令

  ``` bash
  sudo adduser oracle
  sudo usermod -u 54321 oracle
  sudo groupmod -g 54321 oracle
  ```

- 切换到Oracle账号

  `sudo su - oracle`

- 创建目录并设置权限, 这里是在登陆Oracle之后，只需要在`home/oracle`目录下创建oradata的文件夹, 切忌这里不能用sudo提升权限

 `mkdir oradata`

- 在home下创建docker-compose.yml文件：
``` yml
version: "3"
services:
  oracle:
    container_name: oracle12c
    image: oracle/database:12.2.0.1-ee
    restart: always
    ports:
      - "1521:1521"
      - "5500:5500"
    volumes:
      - /home/oracle/oradata:/opt/oracle/oradata
    shm_size: 1g
    environment:
      # ORACLE_SID: ORCLCDB
      # ORACLE_PDB: ORCLPDB1
      ORACLE_PWD: Hpst1231
      # ORACLE_CHARACTERSET: AL32UTF8
```
- 退出oracle账号，使用user账号(管理员账号)，将oracle账号添加到用户组中

`sudo usermod -aG docker oracle`

- 然后再切换到oracle账号，启动服务

`docker-compose up`

- 如果启动正常的话， 可加参数 -d 让docker在后台运行

  `docker-compose up -d`