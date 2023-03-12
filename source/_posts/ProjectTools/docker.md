---
title: Docker
date: 2012/5/11
categories:
- ProjectTools
---

> Linux 命名空间、控制组和 UnionFS 三大技术支撑了目前 Docker 的实现

### namespaces
命名空间 (namespaces) 是 Linux 为我们提供的用于分离进程树、网络接口、挂载点以及进程间通信等资源的方法。
linux七种不同的命名空间机制，包括 CLONE_NEWCGROUP、CLONE_NEWIPC、CLONE_NEWNET、CLONE_NEWNS、CLONE_NEWPID、CLONE_NEWUSER 和 CLONE_NEWUTS