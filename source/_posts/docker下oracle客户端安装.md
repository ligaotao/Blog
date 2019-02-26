---
title: docker下oracle客户端安装
date: 2019-02-26 09:59:14
tags:
---

> 在docker中安装oracle客户端，需要编辑Dockerfile文件，将oracle客户端放入docker内部

1. 下载Oracle 18,12或11.2“Basic”或“Basic Light”zip文件：[64位](https://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html) 或[32位](https://www.oracle.com/technetwork/topics/linuxsoft-082809.html)，与您的Python体系结构相匹配。

2. 将文件放到Dockerfile同级的目录下，如在其他目录则访问不到

3. 环境依赖需要`libaio1`安装包

4. 以下为Dockerfile文件内容

COPY命令不能拷贝上下文之外的文件
ADD可以添加并自动解压.tar文件

RUN apt-get update && apt-get install zip -y

增加-y是 默认为同意 不然会出现安装失败


```bash
FROM python:3.6-jessie

ENV TNS_ADMIN=/oracle_client/instantclient_18_3
ENV NLS_LANG=SIMPLIFTED_CHINESE_CHINA_ZHS16GBK
ENV LD_LIBRARY_PATH=/oracle_client/instantclient_18_3

# 安装过程需要 一个解压用的zip包 和 oracle项目依赖包libaio1

RUN apt-get update && apt-get install zip -y
RUN apt-get update && apt-get install libaio1 -y

# 创建文件夹 并将oracle客户端移动并解压到该文件夹 这里是将下载的文件重命名成了client.zip

RUN echo \
  && mkdir -p /opt/oracle && cd /opt/oracle \
  && echo

ADD client.zip /opt/oracle
RUN cd /opt/oracle && unzip client.zip

# 如果计算机上没有其他Oracle软件会受到影响，请将Instant Client永久添加到运行时链接路径

RUN sh -c "echo /opt/oracle/instantclient_18_3 > /etc/ld.so.conf.d/oracle-instantclient.conf" \
  && ldconfig

# RUN export LD_LIBRARY_PATH=/opt/oracle/instantclient_18_3:$LD_LIBRARY_PATH

RuN mkdir -p /opt/oracle/instantclient_12_2/network/admin

WORKDIR /usr/src/app

COPY . /usr/src/app
COPY pip.conf /root/.pip/pip.conf
RUN pip install --no-cache-dir -r requirements.txt
RUN touch .env
RUN mkdir -p var/log
RUN python manage.py collectstatic

```


参考文档

1. [cx-oracle官方文档](https://cx-oracle.readthedocs.io/en/latest/installation.html#oracle-instant-client-zip-files)