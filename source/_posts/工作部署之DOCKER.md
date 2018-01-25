
---
title: 工作之Docker部署
date: 2018-01-24 10:59:35
tags:
categories: Docker
---


- 切换到Oracle账号

  `sudo su - oracle`

- 创建目录并设置权限, 这里是在登陆Oracle之后，只需要在home目录下创建oradata的文件夹

 `sudo mkdir oradata`

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