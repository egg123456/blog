---
title: 搭建LAMP
date: 2018/5/12
---
# 安装Apache
```bash
sudo apt-get install apache2

测试： 浏览器访问http://Ubuntu的IP，出现It Works!网页。

查看状态： service apache2 status/start/stop/restart

Web目录： /var/www

安装目录： /etc/apache2/

全局配置： /etc/apache2/apache2.conf

监听端口： /etc/apache2/ports.conf

虚拟主机： /etc/apache2/sites-enabled/000-default.conf
```

# 安装MySQL
sudo apt-get install mysql-server mysql-client

测试：mysql -u root -p
    在MySQL>提示符下时 输入quit/Ctrl+D 退出

查看状态：service mysql status/start/stop/retart

查看监听端口的情况：netstat -tunpl 或 netstat -tap

# 安装PHP
sudo apt-get install php7.0

测试：php7.0 -v

# 安装其他模块
sudo apt-get install libapache2-mod-php7.0
sudo apt-get install php7.0-mysql

重启服务

service apache2 restart

service mysql restart

测试Apache能否解析PHP

vim /var/www/html/phpinfo.php
默认是输入控制命令的模式，按 i 键进入编辑模式。按Esc退回命令模式。在命令模式下：wq保存并退出vim

文件中写：<?php echo phpinfo();?>

浏览器访问：http://ubuntu地址/phpinfo.php，出现PHP Version网页

# 修改权限
sudo chmod 777 /var/www

# 安装phpMyAdmin
sudo apt-get install phpmyadmin

安装：选择apache2，点击确定。下一步选择是要配置数据库，并输入密码。

创建phpMyAdmin符号链接：sudo ln -s /usr/share/phpmyadmin /var/www/html

启用Apache mod_rewrite模块：sudo a2enmod rewrite

重启服务：

service php7.0-fpm restart

service apache2 restart

测试：浏览器访问：http://ubuntu地址/phpmyadmin

# 配置Apache
vim /etc/apache2/apache2.conf

添加：

AddType application/x-httpd-php .php .htm .html

AddDefaultCharset UTF-8

重启Apache服务


# 服务器
120.78.164.160  root EG-yeg123