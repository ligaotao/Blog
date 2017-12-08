---
title: https升级之路
date: 2017-12-08 16:02:15
tags:
categories: nginx
---

> 现在是全站https的时代，如果不升级https，有的地方是不允许使用的http协议的，就像小程序都是不允许的，所有有了我这一波升级

## 获取证书

在[FreeSSL](https://freessl.org)这个网站上我们可以轻松获取一年的免费证书

输入我们的域名 然后邮箱 后会进行域名的验证，

这里验证我们选择了手动验证（DNS）

通过在域名管理哪里建立一条解析的规则

![域名认证](/images/域名验证.png)

验证通过后我们就得到了两个 一个是`pem`的公钥，一个是`key`的私钥

## 通过nginx设置

```config

        server {
                listen 443;
                server_name mp.ligaotao.cn;
                ssl on;
                # /path/to 是我们公钥存放的路径
                ssl_certificate /path/to/server.pem;
                ssl_certificate_key /path/to/server.key;
                location / {
                        root /home/ligaotao/blog;
                        index index.html;
                        try_files $uri $uri/ /index.html;
                }
        }



```


然后重启nginx服务就看到了https的标志