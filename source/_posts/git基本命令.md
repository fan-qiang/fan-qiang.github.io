---
title: git基本命令
date: 2018-07-25 12:55:08
tags: git
categories: scm
---

一些git 基本命令介绍：

## git init

要对现有的某个项目开始用 Git 管理，只需到此项目所在的目录，执行：

```bash
$ git init
```

该命令创建一个空的Git仓库 - 基本上是创建一个具有`objects`，`refs/head`，`refs/tags`和模板文件的`.git`目录。 还创建了引用主分支的`HEAD`初始的一个`HEAD`文件。

## git add

命令将文件内容添加到索引(将修改添加到暂存区)。也就是将要提交的文件的信息添加到索引库中。

```bash
$ git add . # 所有文件加入索引库
$ git add *.js #将所有js文件加入索引库
```



## git commit

命令用于将更改记录(提交)到存储库。将索引的当前内容与描述更改的用户和日志消息一起存储在新的提交中。

git commit 的常用参数

```bash
$ git commit -m '修改样式' # 提交注释信息
$ git commit -v # 提交时显示所有diff信息
```

## 一些有用的git学习网站

[learngitbranching](https://learngitbranching.js.org) 一个通过图形界面学习的网站

[阮一峰git操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)

[git-scm 文档](https://www.git-scm.com/doc)

