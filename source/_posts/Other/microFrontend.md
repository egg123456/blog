---
title: micro frontend
date: 2018/5/3
categories:
- Other
---

> 微前端，早已是一个老生常谈的概念，它于 2016 年首次出现在 ThoughtWorks Technology Radar 上，将后端微服务的概念扩展到了前端世界。具体来讲，就是将一个单体应用，按照一定的规则拆分为一组服务。这些服务，各自拥有自己的仓库，可以独立开发、独立部署，有独立的边界，可以由不同的团队来管理，甚至可以使用不同的编程语言来编写。但对前端来说，仍然是一个完整的服务。

### The challenges faced by micro front-end
1. 子应用切换；
2. 应用相互隔离，互不干扰；
3. 子应用之间通信；
4. 多个子应用并存；
5. 用户状态的存储 - 免登；


### Common technical solutions for micro front-end
1. 路由分发式微前端
路由分发式微前端，即通过路由将不同的业务分发到不同的独立前端应用上。最常用的方案是通过 HTTP 服务的反向代理来实现。
下面是一个基于路由分发的 Nginx 配置：
```
http {
  server {
    listen 80;
    server_name  xxx.xxx.com;
    location /api/ {
        proxy_pass http://localhost:3001/api;
    }
    location /web/admin {
        proxy_pass http://localhost:3002/api;
    }
    location / {
        proxy_pass /;
    }
  }
}
```

2. iframe
3. single-spa
4. qiankun
5. webpack5：module federation
6. Web Component


