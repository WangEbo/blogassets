---
title: 前端必知扩展☞HTTP协议
date: 2017-10-28 20:22:37
tags: [http协议]
---

#### http协议概念

- http(HyperText Transfer Protocol)：超文本传输协议，web服务器上储存有html文件及图像资源等，在请求资源时，客户的（浏览器端）与web服务器端之间的交互协议；它是基于TCP/IP协议的应用层协议，不涉及数据包(packet)传输，默认端口为80

#### http协议的特点

1. 支持B/S(browser / server) 和 C/S (client / server) 两种结构的访问

2. 无连接请求

   - http1.0中，（短连接）每次TCP/IP连接只能处理一个请求，即一次请求对饮返回一次响应就断开连接

   - http1.1中，（长连接）一次请求可以请求多个资源

     > 如Connection：keep-alive。keep-alive功能使客户端到服务器端的连接持续有效，当出现对服务器的后续请求时，keep-alive功能避免了重新建立连接

3. 无状态

   - 同一个浏览器向同一服务器发起多次请求的时候，服务器不能识别该浏览器（因此需要cookie来记录状态）

#### 请求协议组成部分

- 请求行

  用一行来说明当前请求的基本信息

  > GET || post   url   HTTP/1.1

- 请求头

  请求中当前要用到的协议向的集合，即浏览器在发送请求数据之前，事先告诉浏览器的信息（通常是浏览器自身的信息），每个协议独占一行

  >host：当前url中请求服务器的主机名（域名）
  >
  >accept：标识浏览器可以接受的数据类型（MIME类型）如text/html、text/css、text/javascript、image/png等等
  >
  >accept-language：可以接受的语言类型：zh-cn，en，fr等
  >
  >user-agent：用户代理UA，当前发起请求的浏览器内核信息，作为识别客户端设备的重要信息。如：
  >
  >​                      Agent: Mozilla/5.0、Gecko/20100101、winNT6.1-win7
  >
  >referer：此次请求来自的网址：可以判断请求是否来自本网站，防止盗链

- 空白行

- 请求体

  主要是通过表单提交的数据，只有通过post请求提交的数据才会在请求体中出现，**一般使用application/x-www-form-urlencoded对表单数据进行编码，文件上传时必须使用multipart/form-data方式**

#### 从http协议角度看get和post差异

- 请求数据查看位置		  请求头		请求体
- 安全性                                低                    高
- 数据上限                            1kb                   8M
- 历史记录中能否看到参数    是                      否

#### 响应协议的组成

- 响应头
- 空白行
- 响应体

#### 会话技术

- 会话：浏览器与服务器之间的数据交互
- 会话技术：在同一台浏览器对服务器的多次请求中，将数据持久化存储的技术，以实现连续的业务逻辑

#### 会话技术分类

- 数据持久存储在服务器，session技术
- 数据持久存储在浏览器，cookie技术

#### cookie

- Cookies是服务器在本地机器上存储的小段文本并随每一个请求发送至同一个服务器。IETF RFC 2965 HTTP State Management Mechanism 是通用cookie规范。
- 正统的cookie分发是通过扩展HTTP协议来实现的，服务器通过在HTTP的响应头中加上一行特殊的指示以提示浏览器按照指示生成相应的cookie。然而纯粹的客户端脚本如JavaScript也可以生成cookie。而cookie的使用是由浏览器按照一定的原则在后台自动发送给服务器的
- cookie本质是是string类型的数据
- cookie的内容主要包括：名字，值，过期时间，路径和域，
- cookie数据是基于浏览器的，同一浏览器访问同一域名下的不同页面cookie可共享，但不同浏览器访问同一页面，cookie不可共享。cookie若不设置过期时间，则表示这个cookie的生命期为浏览器会话期间，关闭浏览器窗口，cookie就消失。若设置了过期时间，浏览器就会把cookie保存到硬盘上，关闭后再次打开浏览器，这些cookie仍然有效直到超过设定的过期时间。存储在硬盘上的cookie可以在不同的浏览器进程间共享，比如两个IE窗口。而对于保存在内存里的cookie，不同的浏览器有不同的处理方式。

#### session

- session机制是一种服务器端的机制，服务器使用一种类似于散列表的结构，可以存放几乎所有类型的数据
- session存放于服务器端内存文件中，可供同一域名下多个页面共享
- session是基于cookie的