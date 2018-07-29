---
title: HTTP 简介
p: http/http-简介
date: 2018-07-27 22:22:15
tags: HTTP
categories: 前端
---

## HTTP 简介

HTTP (HyperText Transfer Protocol HTTP) 超文本传输协议是一种分布式、协作式和和超媒体的应用层协议，是在网络上进行数据传输的协议。

## web服务器与客户端

在互联网上web资源存储在web服务器上，而这些服务使用的是http协议，客户端则通过http协议去访问服务端的资源与内容。一个常见的场景是客户端 向服务器端发送http请求某个资源，服务器端通过http协议返回资源的内容。

### 资源访问

在互联网中webserver对外提供可访问的资源，用户通过标识定位并访问具体资源。

#### URI

​	统一资源标识符(Uniform Resource Identifier，URI) ，是一个用于表示某一互联网资源的字符串。URI有两种形式 URL(统一资源定位) ，URN(统一资源名称)，URL如同一个人的地址，URN则如同一个人的名字。因为在使用URL使用的范围更为广泛的原因在大多数的时候URI 等同于 URL。

#### URL

​	统一资源资源定位符(URL) 描述的资源的具体地址。她描述了一个特定服务器上的的一个特定资源的位置。

```http
https://www.colorful.com/images/today.jpg 
```

👆资源表示通过`https`协议访问的`www.colorful.com` 网站 `images`路径下的`today.jpg`图片。

URL分为主要三个部分:

1. scheme  访问资源的协议类型。
2. 服务器的地址域名 (如www.colorful.com)
3. 资源的路径  (/images/today.jpg)

#### URN

​	统一资源名称,URN是作为特定内容的唯一名称使用。基于URN的概念一个资源通过他的唯一名称去访问，改资源的位置则灵活的迁移，这是URN相对于URL的好处。

```http
urn:ietf:rfc:2141
```

👆表示表示了RFC 2141 文档的URN名称。

## URL资源

URL的语法

```http
<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
```

|   组件   |                描述                |                             关注                             |
| :------: | :--------------------------------: | :----------------------------------------------------------: |
|  scheme  |         与服务器交互的协议         |                                                              |
|   user   |         部分协议需要用户名         |                      ftp等协议需要此项                       |
| passowrd |          部分协议需要密码          |                                                              |
|   host   |           主机名或ip地址           | 在互联网访问中通常为域名，部分情况下使用主机名或ip如 localhost |
|   port   |               端口号               |                      http协议默认端口80                      |
|   path   |        资源在服务器上的路径        |                                                              |
|  param   |                参数                |                                                              |
|  query   |              查询参数              |                                                              |
|   frag   | 片段，引用资源的时候使用其中的部分 |        在http中的html网页中通常指页面上的某个元素的id        |

http使用的url常用格式

```http
http://domain.name[:port]/resource[;param=v]?param1=v1&param2=v2#element_id
```



## HTTP的报文结构

http的报文结构分为三个部分：

1. start line 起始行

2. header 报文头

   header部分为 k:v的键值对，http协议包含了大量的请求头部信息。

3. body body为可选部分

### HTTP请求报文 request

#### 报文格式：

```http
<method> <request-URL> <version> 
<headers>
                                     * 注意这个空行
<entity-body>
```

一个示例：

通过curl命令访问baidu.com:

```bash
$ curl -s -v -H 'special:xxx' www.baidu.com
```

http头内容 

```http
> GET / HTTP/1.1           
> Host: www.baidu.com
> User-Agent: curl/7.54.0
> Accept: */*
> special:xx
>
```

报文的内容分析

1. GET / HTTP/1.1 报文起始行 
   * GET http method 
   * / request-URL
   * HTTP/1.1 http的1.1版本
2. 报文头 
   * Host: www.baidu.com 
   * User-Agent: curl/7.54.0 
   * Accept: */* 
   * special:xx
3. 空行 （用于区分报文头与报文体的内容）
4. 报文体 为空 本次请求并没有携带报文体

### HTTP响应报文 response

HTTP响应报文与请求报文基本相同

#### 报文格式：

```http
<version> <status> <reason-phrase>
<headers>
								 * 注意这个空行
<entity-body>
```

仍以上一节中的发送请求的举例

```bash 
$ curl -s -v -H 'special:xxx' www.baidu.com
```

返回报文的内容 

```http
< HTTP/1.1 200 OK
< Server: bfe/1.0.8.18
< Date: Sat, 28 Jul 2018 03:15:33 GMT
< Content-Type: text/html
< Content-Length: 2381
< Last-Modified: Mon, 23 Jan 2017 13:28:24 GMT
< Connection: Keep-Alive
< ETag: "588604f8-94d"
< Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
< Pragma: no-cache
< Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/
< Accept-Ranges: bytes
<
<!DOCTYPE html>
<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=http://s1.bdstatic.com/r/www/cache/bdorz/baidu.min.css><title>百度一下，你就知道</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=百度一下 class="bg s_btn"></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>新闻</a> <a href=http://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>地图</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>视频</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>贴吧</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>登录</a> </noscript> <script>document.write('<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ '" name="tj_login" class="lb">登录</a>');</script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">更多产品</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>关于百度</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>使用百度前必读</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>意见反馈</a>&nbsp;京ICP证030173号&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>
```

返回报文分析:

1. HTTP/1.1 200 OK 报文起始行 

   - HTTP/1.1 http的1.1版本
   - 200 status状态码
   - OK reason-phrase 状态码原因

2. 报文头 

   * Server: bfe/1.0.8.18 < Date: Sat, 28 Jul 2018 03:15:33 GMT 
   * Content-Type: text/html 
   * Content-Length: 2381 
   * Last-Modified: Mon, 23 Jan 2017 13:28:24 GMT 
   * Connection: Keep-Alive
   * ETag: "588604f8-94d" 
   * Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform 
   * Pragma: no-cache 
   * Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/ 
   * Accept-Ranges: bytes

3. 空行 （用于区分报文头与报文体的内容）

4. 报文体 

   <!DOCTYPE html> 至报文结束

### 使用工具查看HTTP请求

#### chrome开发者工具	

打开chrome 访问 网站 如  www.baidu.com

通过快捷键 `command + alt + i` 打开`开发者工具` 切换至 `network`页签，查看网页中访问的请求，在右侧查看请求与响应的内容。

![chrome调试](chrome-dev.png)

#### curl

curl一款基于命令行或脚本传输的数据的工具 ，curl 通过url 定位资源。curl的使用方式:

```bash
$ curl [options] [URL...]
```

`常用参数`

* -u < user[:password] > 设置用户名密码
* -v 显示更详细的操作信息
* -s 静默模式
* -H 设置head中的值与数据

`使用示例`

1. 发送普通请求

   ```http
   $ curl www.baidu.com
   ```

2. 设置head中的值

   ```bash
   curl -H "Content-Type:application/json" www.baidu.com
   ```

3. 设置方法

   ```http
   curl -X POST www.baidu.com
   curl -X PUT www.baidu.com
   ```