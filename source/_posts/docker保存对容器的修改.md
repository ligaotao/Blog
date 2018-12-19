---
title: docker保存对容器的修改
date: 2018-12-19 09:57:42
tags:
categories: Docker
---

> 在docker中修改内容后，重启后发现修改内容并没有得到保存

1. 修改完毕后，再打开一个终端执行

```bash
docker ps
# 输出内容为
# CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
# 96621f37028c        0ef2e08ed3fa        "/bin/bash"         3 minutes ago       Up 3 minutes                            thirsty_torvalds
```

2. 得到CONTAINER ID 及 IMAGE 名称, 进行提交

```bash
docker commit 96621f37028c 0ef2e08ed3fa
# 输出为 sha256:919694de9dda0f070de8839284e0a3b8f03e9bf88207111e144986d3aaefb2a9
```

3. 查看images就能看到刚才修改记录

```bash
docker images
# 输出
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	0ef2e08ed3fa        latest              919694de9dda        13 seconds ago      130 MB
	<none>              <none>              1fce756b350f        3 minutes ago       130 MB
	zzq/ubuntu          test                0ef2e08ed3fa        5 weeks ago         130 MB
	ubuntu              latest              0ef2e08ed3fa        5 weeks ago         130 MB
	hello-world         latest              48b5124b2768        2 months ago        1.84 kB
```

4. 现在 已经实现保存了