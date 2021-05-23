---
title: jumpserver
date: 2018/5/2
categories:
- os
---

# 跳板机
跳板机就是一台服务器，卡发或运维人员在维护过程中首先要统一登陆到这台服务器，然后再登陆到目标设备进行维护和操作。
tips：跳板机没有实现对运维人员操作欣慰的控制和审计，使用跳板机的过程中还是会出现误操作、违规操作导致的事故，一旦出现操作事故很难快速定位到原因和责任人。

# 堡垒机
堡垒机，即在一个特定的网络环境下，为了保障网络和数据不受来自外部和内部用户的入侵和破环，而运用各种技术手段实时收集和监控网络环境中每一个组成部分的系统状态、安全事件、网络活动，以便集中报警，及时处理及审计定则。
tips：堡垒机比跳板机多了实时收集、监控网络环境、集中报警等功能

# xshell
+ Xshell 是一个强大的安全终端模拟软件，它支持SSH1, SSH2, 以及Microsoft Windows 平台的TELNET 协议。Xshell 通过互联网到远程主机的安全连接以及它创新性的设计和特色帮助用户在复杂的网络环境中享受他们的工作。
+ Xshell可以在Windows界面下用来访问远端不同系统下的服务器，从而比较好的达到远程控制终端的目的。除此之外，其还有丰富的外观配色方案以及样式选择。

# jumpserver堡垒机组件
+ jumpserver：现指jumpserver管理后台、是核心组件，使用 Django Class Based View 风格开发，支持 Restful API。
+ Coco： 实现了 SSH Server 和 Web Terminal Server 的组件，提供 SSH 和 WebSocket接口，使用 Paramike 和 Flash 开发。
+ luna： 现在是 Web Terminal 前端，计划前端页面都由该项目提供、Jumpserver 指提供API ,不在负责后台渲染html等


## command
+ getenforce命令           
使用getenforce命令可以显示当前SELinux的应用模式，是强制、执行还是停用。
命令语法：getenforce
+ systemctl 服务管理工具
systemctl stop firewalled 暂停防火墙
systemctl disable firewalled.service 禁用防火墙

# wget 
是一个从网络上自动下载文件的自由工具，支持通过 HTTP、HTTPS、FTP 三个最常见的 TCP/IP协议 下载，并可以使用 HTTP 代理。"wget" 这个名称来源于 “World Wide Web” 与 “get” 的结合。


# linux 通过源代码 安装程序 
1. 下载源码
2. 解压缩   tar xvf python-3.6.1.tar。xz
3. 执行 ./configure (编译生成makefile)
4. make 操作makefile
5. make install （安装）

# pip 

# visudo
visudo使用vi打开/etc/sudoers文件，但是在保存退出时，visudo会检查内部语法，避免用户输入错误信息

# tail
tail -f notes.log 此命令显示 notes.log 文件的最后 10 行。当将某些行添加至 notes.log 文件时，tail 命令会继续显示这些行。 显示一直继续，直到您按下（Ctrl-C）组合键停止显示。

# whoami 用于显示自身用户名称

# ifconfig命令用于显示或设置网络设备

# 用户分类
+ jumpserver用户：用来登陆jumpserver（web界面、ssh登陆）
+ 管理用户： 用来自动创建客户机上的系统用户、批量执行命令等操作
+ 客户机上的系统用户： 用来通过jumpserver去登录每一台客户机的用户