---
title: 使用Travis CI来自动部署你的Hexo博客
date: 2017-06-08 18:38:09
tags:
categories: 工具类
---

# 使用Travis CI来自动部署你的Hexo博客

## 简介

> 之前使用博客都需要手动调用`hexo generate`来生成静态的`html`，然后再通过`git`提交到`github`，现在，使用`Travis CI`就可以进行自动部署，仅仅需要将`md`文件提交给`git`, 其他就交给`Travis CI`就行了，剩下的时间就可以找女朋友去了！棒棒哒！

## Travis CI

Travis CI 是目前新兴的开源持续集成构建项目，它与[jenkins](http://baike.baidu.com/item/jenkins)，GO的很明显的特别在于采用[yaml](http://baike.baidu.com/item/yaml)格式，简洁清新独树一帜。目前大多数的[github](http://baike.baidu.com/item/github)项目都已经移入到Travis CI的构建队列中，据说Travis CI每天运行超过4000次完整构建。

## 开始

1. 登陆[Travis CI](https://travis-ci.org/)

2. 关联我们在`github`的项目

3. 在我们项目的更目录下增加`.travis.yml`文件

   ```yaml
   language: node_js # 语言
   node_js:
     - "7" # nodejs 版本
   script:
       - hexo generate # 执行的脚本命令
   install:
       - npm install # 安装命令
   before_install:
       - "npm install -g hexo-cli" # 安装前执行
   after_install:
   after_script: # 执行脚本命令后钩子
     - cd ./public
     - git init
     - git config user.name "流水"
     - git config user.email "774206981@qq.com"
     - git add .
     - git commit -m "更新文章"
     - git push --force --quiet "https://${GITHUB_TOKEN}@${GITHUB_REF}" master:master
   branches: # 影响分支
     only:
       - pages
   cache:
     directories:
       - "node_modules"
   ```

   注：1.  `GITHUB_TOKEN`与`GITHUB_REF`是在`Travis CI`配置的环境变量

   注：2. 我们的开发分支在pages, 构建后的分支为主分支

## Travis CI 配置

### general

- [x] Build only if .travis.yml is present
- [x] Build branch updates
- [x] Build pull request updates
- [ ] Limit concurrent jobs

### Environment Variables

> 可以增加一些环境变量 可以在yml文件中使用



## 大功告成

现在我们可以愉快的写博客了