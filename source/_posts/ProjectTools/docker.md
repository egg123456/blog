---
title: Docker
date: 2012/5/11
categories:
- ProjectTools
---

> Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从 Apache2.0 协议开源。

## Linux 命名空间、控制组和 UnionFS 三大技术支撑了目前 Docker 的实现

### namespaces
命名空间 (namespaces) 是 Linux 为我们提供的用于分离进程树、网络接口、挂载点以及进程间通信等资源的方法。
linux七种不同的命名空间机制，包括 CLONE_NEWCGROUP、CLONE_NEWIPC、CLONE_NEWNET、CLONE_NEWNS、CLONE_NEWPID、CLONE_NEWUSER 和 CLONE_NEWUTS


## Docker 包括三个基本概念
1. 镜像（Image）：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
2. 容器（Container）：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
3. 仓库（Repository）：仓库可看成一个代码控制中心，用来保存镜像。

## 启动虚拟机/启动windows下的linux子系统
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart


# command
```shell
docker run -d --name localMysql -p 3306:3306 -e TZ=Asia/Shanghai -e MYSQL_ROOT_PASSWORD mysql
# docker run 创建并运行一个容器，-d 是让容器在后台运行
# --name localMysql 给容器起个名字，必须唯一
# -p 3306:3306 设置宿主机与容器端口映射
# -e 设置容器的环境变量
# mysql 值得是镜像名
# 即这里以mysql镜像创建并运行了一个叫localMysql的mysql容器，环境变量有时区、root账号密码

# 停止容器
docker stop localMysql

# 查看运行中的容器 -a 表示所有（既包含暂停的容器）
docker ps -a

# 停止恢复
docker start localMysql

# 容器日志 -f 表示持续查看日志
docker logs localMysql

# 以bash交互终端形式进入容器内部
docker exec -it localMysql bash

# 删除容器 -f 表示强制删除、不管容器是否在运行
docker rm localMysql -f
```

## 修改镜像源
```shell
vim /etc/docker/daemon.json
# {
#   "registry-mirrors":[
#     "https://docker.rainbond.cc"              
#   ]
# }

# 重启docker
sudo systemctl daemon-reload
sudo systemctl restart docker
```
tips: 当docker pull 失败、超时时可修改源


# dockerfile 
dockerfile 就是一个文件，其中包含一个个的指令(instruction)，用指令来说明要执行什么操作来构建镜像。
常见指令如下：
指令 | 说明 | 示例
------|-----|-----
FROM | 指定基础镜像 | FROM centos:6
ENV | 设置环境变量、可在后面指令使用 | ENV key value
COPY | 拷贝本地文件到镜像的制定目录 | COPY ./dist /var/nginx/html
RUN | 执行Linux的shell命令，一般是安装过程的命令 | RUN npm i
EXPOSE | 指定容器运行时监听的端口，是给镜像使用者看的 | EXPOSE 8080
ENTRYPOINT | 镜像中应用的启动命令，容器运行时调用 | ENTRYPOINT node ./start.js

```shell
# 使用官方MySQL镜像
FROM mysql:5.7
 
# 设置环境变量，包括数据库名、用户和密码
ENV MYSQL_DATABASE=mydatabase
ENV MYSQL_USER=myuser
ENV MYSQL_PASSWORD=mypassword
ENV MYSQL_ROOT_PASSWORD=myrootpassword
 
# 创建一个数据卷以持久化数据库数据
VOLUME /var/lib/mysql
 
# 容器启动时初始化数据库和用户
COPY init.sql /docker-entrypoint-initdb.d/
 
# 容器启动时默认运行MySQL服务
CMD ["mysqld"]
```

## command
```shell
# 
docker save -o ./jdk.tar

# 加载本地jdk镜像
docker load -i ./jdk.tar

# dockerfile 目录下构建镜像
docker build -t test-image .

# 查看镜像
docker images

# 删除镜像
docker rmi test-image
# 删除 none 镜像
docker rmi $(docker images -f "dangling=true" -q)

```


# docker compose
docker compose 通过一个单独的docker-compose.yml模板文件（YAML格式）来定义一组相关联的应用容器，帮助我们实现多个相互关联的Docker容器的快速部署。
```shell
# up 创建并启动所有service容器
# down 停止并移除苏哦有容器、网络
# ps 列出所有启动的容器
# logs 查看指定容器的日志
# stop 停止容器
# start 启动容器
# restart 重启容器
# top 查看运行的进程
# exec 在指定的运行中容器中执行命令
docker compose -f [dockerComposeFilePath] -p [projectName] up
```

docker-compose.yml
```shell
version: '3'
 
services:
  express-server:
    # dockFile 文件所在目录
    build:
      context: .
      dockerfile: ./dockerfile
    container_name: express-server
    ports:
      - "3000:3000"
    environment:
      MYSQL_HOST: mysql-server
      MYSQL_ROOT_PASSWORD: password
    # 仅当容器以非零退出码退出时重启
    restart: on-failure
    depends_on:
      - mysql-server
    networks:
      - custom-netWork
 
  mysql-server:
    image: mysql:5.7
    container_name: mysql-server
    ports:
      - 3306:3306
    environment:
      TZ: Asia/Shanghai
      MYSQL_ROOT_PASSWORD: rootPassword
    volumes:
      - "./mysql/conf:/etc/mysql/conf.d"
      - "./mysql/data:/val/lib/mysql"
      - "./mysql/init:/docker-entrypoint-initDB.d"
    networks:
      - custom-netWork

  nginx-server:
    build: ./nginx
    volumes:
      - "./nginx/nginx.conf:/etc/nginx/nginx.conf"
      - "./nginx/html:/usr/share/nginx/html"
    ports:
      - "80:80"
    depends_on:
      - express-server
    networks:
      - custom-netWork
 
  react-client:
    # dockerfile 文件目录
    build: ./react-app
    ports:
      - "5000:5000"
    networks:
      - custom-netWork

networks:
  custom-netWork:
    name: eggNet
```

# docker cache clear
```shell
# 清空所有未使用的容器、网络、数据卷等
docker system prune

# 清空所有未使用的容器
docker container prune

# 清空所有未使用的数据卷
docker volume prune

# 清空所有未使用的网络
docker network prune
```

docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=123456 -v /mnt/c/Users/18797/ws/mysql/data:/var/lib/mysql mysql:5.7