---
title: nginx
date: 2018/5/14
categories:
- OS
---

Nginx的配置文件（nginx.conf）整体上分为几个部分：全局块、events块、http块、server块和location块。
全局块：配置影响Nginx全局的指令，如用户组、进程数、日志路径等；
events块：配置网络连接；
http块：配置代理、缓存、日志记录等；
server块：配置虚拟主机；
location块：配置请求的路由和处理情况。

### getting start 
```shell
# 默认安装
sudo apt install nginx
# 验证nginx服务是否启动
curl http://127.0.0.1
# 启动
sudo systemctl start nginx
# 停止
sudo systemctl stop nginx
# 重启
sudo systemctl restart nginx
```

### nginx 文件存放目录
    path | desc
----------|-------
/var/log/nginx | nginx 运行日志目录
/var/www/html | web项目目录
/usr/sbin/nginx | 服务文件
/etc/nginx | 配置文件目录


### nginx config
```shell
server {
  listen 80;
	server_name www.egg.com;

	location / {
		proxy_pass http://localhost:4000
	}
}
```

