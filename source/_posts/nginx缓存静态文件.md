---
title: nginx缓存静态文件
date: 2017-11-16 10:59:10
tags:
categories: nodejs
---

## 静态文件缓存

> 当页面中的资源不经常变化的时候，可以让资源可以被浏览器能够缓存，下次加载的时候从本地加载，能够显著提高网站的访问速度

`nginx`下的配置如下

``` python
http {
  server {
    location ~* \.(gif|jpg|png|css|js|flv|ico|swf)(.*) {
            proxy_pass http://127.0.0.1:8080; //这里由于使用了反向代理所以资源也需要代理
            expires 30d;
    }
  }
}

```