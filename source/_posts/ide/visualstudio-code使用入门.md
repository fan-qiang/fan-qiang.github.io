---
title: visual studio code 使用入门
p: ide/visualstudio-code使用入门
date: 2018-07-25 19:53:29
tags: visual studio code
categories: IDE
---

Visual Studio Code 是一款跨平台的ide，可以在mac os上进行代码开发与管理，支持多种开发语言如`javascript`  `typescript` `python` 等。可以通过插件的方式进行扩展。

[Visual Studio Code 官网](https://code.visualstudio.com)

mac上的安装比较简单，下载完后直接拖到 `应用程序` 目录中即可。

## 常用操作

### 打开 user settings

```bash
command + , 
```

可以在user settings 中进行配置，基于json个的配置文件。

以下为一些常用的配置

```json
// 以像素为单位控制字号。
"editor.fontSize": 12,
// 控制字体系列。
"editor.fontFamily": "Menlo, Monaco, 'Courier New', monospace",
```

### 打开快捷键列表

```bash
command + K command + s
```

可以在快捷键列表中搜寻对应的快捷键。

### 打开扩展插件的窗口

```bash
command + shift + x
```

如果安装一个open in github 插件，在插件查询中输入open 选择对应的插件进行安装

### Emmet

visual studio code 对 Emmet 提供了良好的支持。默认使用 `tab` 键触发。

