---
title: fromBrowser
date: 2018/5/2
categories:
- base
---


### overview
```flow
st=>start: Start
inputAddr=>operation: 输入地址
isDomain=>condition: 是域名地址
DNSParse=>operation: 域名解析以获取ip
hsaCacheInBrowse=>condition: 浏览器有域名ip缓存吗？
hasCacheInOS=>condition: 系统有域名ip缓存吗？
hostsFile=>condition: hosts 文件有映射吗？
requestDomainServer=>operation: 请求域名服务器，查找对应ip
getIP=>operation: 获得目标ip
hasCache=>condition: 有资源缓存吗？
isFresh=>condition: 缓存是新鲜的吗？
useCache=>condition: 使用缓存
sendRequest=>operation: 发送请求
reseiveRequest=>operation: 服务端接受请求
dealRequest=>operation: 处理请求(查数据库，修改等)
response=>operation: 响应请求
receiveResponse=>operation: 客户端接受响应
dealResponse=>operation: 处理响应(读取html、js、css等文件信心，构建渲染树，读取表单数据等)
e=>end
st->inputAddr->isDomain(yes)->DNSParse->getIP->hasCache(no)->sendRequest->reseiveRequest->dealRequest->response->receiveResponse->dealResponse->e
isDomain(no)->getIP
hasCache(yes)->isFresh(yes)->useCache->dealResponse
isFresh(no)->dealResponse
```

### domain parse
```flow
st=>start: Start
DNSParse=>operation: 域名解析以获取ip
hsaCacheInBrowse=>condition: 浏览器有域名ip缓存吗？
hasCacheInOS=>condition: 系统有域名ip缓存吗？
hostsFile=>condition: hosts 文件有映射吗？
requestDomainServer=>operation: 请求域名服务器，查找对应ip
getIP=>operation: 获得目标ip
e=>end
st->DNSParse->hsaCacheInBrowse(no)->hasCacheInOS(no)->hostsFile(no)->requestDomainServer->getIP->e
hsaCacheInBrowse(yes)->getIP->e
hasCacheInOS(yes)->getIP->e
hostsFile(yes)->getIP->e
```

### resource cache
```flow
st=>start: Start
hasCache=>condition: 是否存在缓存
isExpire=>condition: 缓存是否过期
judgeEtag=>condition: 判断Etag
req-if-none-match=>operation: 向服务器请求 if-none-match
judgeLastModified=>condition: 判断last-modified
req-if-modified-since=>operation: 向服务器请求 if-modified-since
resCache=>condition: 服务器响应资源没有变更？
useLocalCache=>operation: 读取本地缓存
reqResource=>operation: 向服务器请求资源
show=>operation: 显示资源
e=>end
st->hasCache(yes)->isExpire(yes)->judgeEtag(yes)->req-if-none-match->resCache(yes)->useLocalCache->show->e
hasCache(no)->reqResource->show
isExpire(no)->useLocalCache
judgeEtag(no)->judgeLastModified(yes)->req-if-modified-since->resCache
```

### tcp 链接 三次握手
1. 客户端发送一个TCP的SYN=1，Seq=X的包到服务器端口
2. 服务器发回SYN=1，ACK=X+1，Seq=Y的响应包
3. 客户端发送ACK=Y+1，Seq=Z


### server deal
1. 服务器接受请求并解析，将请求转发到服务程序
1. 检查HTTP请求头是否包含缓存验证信息，如果验证缓存新鲜，返回304等对应状态码
2. 根据请求执行操作、读写数据库等，将响应报文通过tcp连接发送回浏览器


### TCP连接的四次握手
1. 主动方发送Fin=1，Ack=Z，Seq=X报文
2. 被动方发送ACK=X+1，ACK=X，Seq=Y报文
3. 被动方发送Fin=1，ACK=X，Seq=Y报文
4. 主动方发送ACK=Y,Seq=X报文

### client deal
1. 浏览器检查响应状态码, 是否为1XX，3XX，4XX，5XX，这些情况处理与2XX不同
2. 如果资源可缓存，进行缓存
3. 对响应进行解码（例如gzip压缩)
4. 根据资源类型决定如何处理（假设资源为HTML文档）
5. 解析 html -词法分析然后解析成 dom 树、解析 css 生成 css 规则树、合并成 render 树，然后 layout 、 painting 渲染、复合图层的合成、 GPU 绘制、外链资源的处理、 loaded 和 DOMContentLoaded 等）


#### 构建DOM树
1. Tokenizing：根据HTML规范将字符流解析为标记
2. Lexing：词法分析将标记转换为对象并定义属性和规则
3. DOM construction：根据HTML标记关系将对象组成DOM树

#### 构建CSSOM树
1. Tokenizing：字符流转换为标记流
2. Node：根据标记创建节点
3. CSSOM：节点创建CSSOM树 

#### 根据DOM树和CSSOM树构建渲染树：
1. 从DOM树的根节点遍历所有可见节点，不可见节点包括：
+ script  ,  meta 这样本身不可见的标签。
+ 被css隐藏的节点，如 display ： none 
2. 对每一个可见节点，找到恰当的CSSOM规则并应用
3. 发布可视节点的内容和计算样式


### JS 引擎解析过程
+ 预处理阶段
  + 分号补全
  + 变量提升
+ 执行阶段
  + 生成执行上下文
  + VO 变量对象
  + 作用域链
  + 回收机制等等
    + 标记清除
    + 引用计数

