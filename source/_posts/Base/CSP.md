---
title: Document type defined
date: 2018/5/2
categories: 
- base
---
> CSP 是一种web安全机制，旨在防范和减轻特定类型的攻击，包括跨站脚本（xss）和数据注入等。它通过允许网站管理源定义和实施一系列安全策略，限制页面加载和执行的内容来源，从而减少潜在的安全风险。

## 分类
1. default-src
2. script-src
3. style-src
4. img-src
5. content-src
6. frame-src


httpOnly 是包含在http响应头 set-Cookie 中的附加标志，用于指示浏览器在创建cookie是设置该标志。设置该标志后javascript 脚本就无法访问该cookie。