---
title: linux命令
date: 2018-01-25 09:51:40
tags:
categories: Linux
---

## 查看所属用户组

``` bash
groups
```

### 给用户增加用户组

> -a 是 append的意思 如果不加 -a 执行覆盖操作 不加的话 ligaotao 的 用户组则变为 ligaotao docker

``` bash
sudo usermod -a -G docker ligaotao
```

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

### screen

1. 创建一个screen窗口, `screen -S iterm`

2. 让当前窗口后台,  `ctrl + a + d`

3. 恢复窗口 `screen -r id` id是窗口的id 可以使用`screen -ls` 查看