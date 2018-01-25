---
title: linux命令
date: 2018-01-25 09:51:40
tags:
categories: Linux
---

### 禁止图形界面启动

```bash
sudo systemctl set-default multi-user.target
```

### 移动文件

> 命令格式：mv [-fiv] source destination

参数说明：

- -f:force 强制移动而不询问
- -i:若文件存在，就会询问是否覆盖
- -u:若文件已经存在，且源文件较新，才会更新

### 删除文件夹

1. 文件夹为空的时候 可以直接执行rmdir移除

    ```bash
    rmdir demo
    ```
2. 如果不为空 则可以执行 rm -rf 删除

    ```linux
    rm -rf demo
    ```