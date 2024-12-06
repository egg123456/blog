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
events {}

http {
	server {
		listen 80;
		# server_name www.egg.com;

		location /api/ {
			proxy_pass http://express-server:4000/api/;
			proxy_http_version 1.1;
			proxy_set_header Upgrade $http_upgrade;
			proxy_set_header Connection 'upgrade';
			proxy_set_header Host $host;
			proxy_cache_bypass $http_upgrade;
		}
		location /view/ {
			proxy_pass http://express-server:4000/view/;
			proxy_http_version 1.1;
			proxy_set_header Upgrade $http_upgrade;
			proxy_set_header Connection 'upgrade';
			proxy_set_header Host $host;
			proxy_cache_bypass $http_upgrade;
		}
		# 单页应用独立文件夹nginx代理配置
		location /devView/ {
			alias /usr/share/nginx/html/devView/;
			index index.html index.htm;
			try_files $uri $uri/ /devView/index.html;
		}
		location /users/ {
			proxy_pass http://express-server:4000/users/;
			proxy_http_version 1.1;
			proxy_set_header Upgrade $http_upgrade;
			proxy_set_header Connection 'upgrade';
			proxy_set_header Host $host;
			proxy_cache_bypass $http_upgrade;
		}
		location / {
			root /usr/share/nginx/html;
		}
	}
}
```

