---
title: window下端口转发
date: 2019-01-09 16:39:03
tags:
---

> 端口转发,一台电脑使用了内外网，当其他电脑想要通过本电脑来连接内网中的电脑时，便要使用端口转发技术

这里是使用了window下的netsh工具来进行转发，win7以上自带该工具

1. 查看端口映射
``` bash
netsh interface portproxy show v4tov4
```
2. 添加端口映射, 将本机（192.168.222.145）的15001端口映射到192.168.222.63的81端口
```bash
netsh interface portproxy add v4tov4 listenaddress=192.168.222.145 listenport=15001 connectaddress=192.168.222.63 connectport=81
```
3. 删除端口映射
```
netsh interface portproxy delete v4tov4 listenaddress=192.168.222.145 listenport=15001
```
