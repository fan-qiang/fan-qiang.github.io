---
title: TypeScript安装与配置
date: 2018-07-24 09:29:15
tags: TypeScript
categories: 前端
---

## TypeScript简介

TypeScript是一个javascript的超集，在javascript上增加了类型系统，为javascript增加静态类型与基于类的面向对象编程。

TypeScript 相关网站:

- [TypeScript官网 ](http://www.typescriptlang.org) 
- [TypeScript-github](https://github.com/Microsoft/TypeScript)
- [TypeScript中文](https://www.tslang.cn)

## 安装准备

- node.js
- vs code

## 安装

typescript编译器，将typescript从ts编译为js

```bash
npm install -g typescript 
```

此命令将安装tsserver 到如下目录

```bash 
/usr/local/bin/tsserver
```



ts-node用于nodejs支持typescript

```bash
npm install -g ts-node
```

此命令将安装ts-node到如下目录

```bash
/usr/local/bin/ts-node
```

## 第一个程序：

* 首先创建一个文件夹用于存放项目内容

  ```bash
  $ mkdir ~/typescript
  ```

* 使用vscode打开项目文件夹`~/typescript`

* 使用vscode创建一个helloworld.ts文件并在文件中输入

  ```javascript
  console.log(" hello world! ")
  ```

* 在`~/typescript/`目录下面创建`.vscode/launch.json`文件并设置typescript的配置,需要注意的是你需要将`~/typescript/`做为一个vscode的工作区并进行保存。

  ```json
   {
       "configurations": [
           {
           "name": "ts-node",
           "type": "node",
           "request": "launch",
           "program": "/usr/local/bin/ts-node", //ts-node的安装目录
           "args": ["${relativeFile}"],
           "cwd": "${workspaceRoot}",
           "protocol": "inspector"
           }
       ]
   }
  ```

  在vscode中 按`F5`运行调试helloworld.ts程序,程序在控制台中输出` hello world `

