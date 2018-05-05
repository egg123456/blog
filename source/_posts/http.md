---
title: http及各协议
---

### 对应
ISO|FUNCTION|TCP-IP|PROTOCOL|frame
---|---|---|---|---
应用层|负责用户信息的语义表示|应用层|HTTP、SMTP、FTP、TELNET/SSH|应用程序
表示层|解决实体互连时信息的表示问题及“语法”|
会话层|提供单双、同时会话模式|
传输层|为高低层间提供接口、分流、合段、拼接、分割（端口是传输层的内容、提供进程通信）|传输层|TCP、UDP|操作系统
网络层|路由选择和中继、数据的分段合段（分组传送）|网间互连层|TP、ICMP、ARP
数据链路层|差错检测与恢复|网络接口层|网络接口层利用以太网中的数据链路层进行通信，因此属于接口层。也可以认为是网卡驱动。驱动程序是在操作系统和硬件之间起桥梁作用的软件。|设备驱动与网络接口
物理层|底层硬件bit流
[reference-link](https://blog.csdn.net/linux_ever/article/details/51136723)

### HTTP、socket、tcp

HTTP是应用层的协议，更靠近用户端；TCP是传输层的协议；而socket是从传输层上抽象出来的一个抽象层，本质是接口。HTTP、socket都基于tcp

--------------
> 在http协议中，一个完整的请求由请求行、请求头和实体内容三部分组成，其中，每部分都有各自不同的作用

请求行
位于请求消息的第一行，它包括三部分，分别请求方式、资源路径以及所使用的http协议版本
GET /index.php HTTP/1.1

请求头
Host : localhost
Connection : keep-alive
User-Agent : Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36
Accept : */*
Referer : http://localhost/newproject/ajax/http.html
Accept-Encoding : gzip, deflate, br
Accept-Language : zh-CN,zh;q=0.8
Cookie : optimizelyEndUserId=oeu1509603275408r0.844298339587459; _ga=GA1.1.1979080760.1502939512

http常见请求消息头|含义
---|---
Host|客户端浏览器想要访问的服务器主机
Accept|客户端浏览器支持的数据类型
Accept-Charset|客户端浏览器采用的编码
Accept-Encoding|客户端浏览器支持的数据压缩格式
Accept-Language|客户端浏览器所支持的语言包，可以指定多个
If-Modified-Since|客户端浏览器对资源的最后缓存时间
Referer|客户端浏览器是从哪个页面内取访问服务器的
User-Agent|客户端主机的环境信息，包括使用的操作系统，浏览器版本号等
Cookie|客户端需要带给服务器的数据
Connection|请求完成后，客户端希望是保持连接还是关闭连接
> php中getallheaders()函数用于获取全部的HTTP请求头信息
```php
<?php
    foreach(getallheaders() as $name=>$value){
        echo $name.' : '.$value."<br/>";
    }
?>
```

请求实体
> 即是请求携带的参数 name=erg&psd=jkl