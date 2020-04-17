---
title: npm
date: 2018-5-8
tags:
---
> [node](/2018/05/08/node/) [nvm](http://www.jianshu.com/p/1aa925e3f0d6) [NPM版本控制](http://www.fly63.com/article/detial/2636)

# npm command
command|description
------|-----
$ npm init | 创建package.json
$ npm install | 安装package.json中的依赖模块
$ npm install packagename@latest | 安装最新模块
$ npm install packagename@0.0.1 | 安装指定版模块
$ npm ls packgename | 查看本地模块的版本a
$ npm view packagename@4.3.1 | 查看模块指定版本的依赖等信息
$ npm view packagename repository.url | 查看模块的原文加地址
$ npm list | 查看已安装的模块(-g 可查看全局已安装的模块)
$ npm list --depth=0 packagename | 限制输入的模块层级和模块
$ npm root -g | 查看全局包的安装目录
$ npm install packagename --save 或 -S | 安装模块并把模块的版本信息保存到dependencies（生产环境依赖）中，即你的package.json文件的dependencies字段中；
$ npm install packagename --save-dev 或 -D|安装模块并把模块版本信息保存到devDependencies（开发环境依赖）中，即你的package.json文件的devDependencies字段中；
npm install packagename --save-optional 或 -O | 安装模块并把把模块安装到optionalDependencies（可选环境依赖）中，即你的package.json文件的optionalDependencies字段中。
npm uninstall packagename | 删除包


## 版本的格式
major.minor.patch-tags
主版本号.次版本号.修补版本号-标签或扩展
patch：修复bug，兼容老版本
minor：新增功能，兼容老版本
major：新的架构调整，不兼容老版本
tags：来说明是预发布版本或者测试版本等

### ~version
~ 版本号 ----- 指定主版本号或者次版本号相同
+ 只含主版本 --- 主版本相同；
+ 含有次版本 --- 主版本和次版本号相同

    + ~1.1.2，表示>=1.1.2 <1.2.0，可以是1.1.2，1.1.3，1.1.4，.....，1.1.n

    + ~1.1，表示>=1.1.0 <1.2.0，可以是同上
    + ~1，表示>=1.0.0 <2.0.0，可以是1.0.0，1.0.1，1.0.2，.....，1.0.n，1.1.n，1.2.n，.....，1.n.n

### ^version
^ 版本号 ----- 第一个非零 版本号相同

+ ^1.1.2 ，表示>=1.1.2 <2.0.0，可以是1.1.2，1.1.3，.....，1.1.n，1.2.n，.....，1.n.n

+ ^0.2.3 ，表示>=0.2.3 <0.3.0，可以是0.2.3，0.2.4，.....，0.2.n
+ ^0.0，表示 >=0.0.0 <0.1.0，可以是0.0.0，0.0.1，.....，0.0.n

### 版本标签
标签 | 意义	| 补充
-----|-----|----
demo | demo版本 | 可能用于验证问题的版本
dev | 开发版 | 开发阶段用的，bug 多，体积较大等特点，功能不完善
alpha | α版本 | 用于内部交流或者测试人员测试，bug较多
beta | 测试版(β版本) | 较α版本，有较大的改进，但是还是有bug
gamma | （γ）伽马版本 | 较α和β版本有很大的改进，与稳定版相差无几，用户可使用
trial | 试用版本 | 本软件通常都有时间限制，过期之后用户如果希望继续使用，一般得交纳一定的费用进行注册或购买。有些试用版软件还在功能上做了一定的限制。
stable | 稳定版 | 
csp | 内容安全装版 | js库常用
latest | 最新版本 |	不指定版本和标签，默认安装新版


-----------------

# yarn 
command | discription
--------|------------
yarn init | 初始化项目
yarn add packgename | 添加依赖包
yarn upgrade packagename | 升级依赖包
yarn remove packgename | 移除依赖包
yarn / yarn install | 安装项目全部依赖
yarn run start | 运行packge.json中定义的脚本

Dependency category | discription
-------------------|-----------
yarn add [package] --dev | devDependencies
yarn add [package] --peer |peerDependencies 
yarn add [package] --optional | optionalDependencies