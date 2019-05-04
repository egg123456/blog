---
title: vue-router
date: 2018/5/11
categories:
- js library
---
# vue-cli
```shell
# 全局安装 vue-cli
$ cnpm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
$ vue init webpack my-project
# 这里需要进行一些配置，默认回车即可
This will install Vue 2.x version of the template.
```

## 路由传参
1. 标签形式
```html
<router-link :to="{path:'/home',query:{name:'eg'}}">
```
```js
//指向组件的方法中获得参数
this.$route.query.name
```
2. 代码形式
```js
this.$router.push({ path: 'home', query: { name: this.name }});
```
```js
//指向组件的方法中获得参数
this.$route.query.name
```
3. 路由配置形式
```js
//路由配置
{
    path: '/describe/:id',
    name: 'Describe',
    component: Describe
}
```
```js
this.$router.push({path: `/describe/${id}`,})
```
```js
//指向组件的方法中获得参数
this.$route.params.id
```


# vuex
> 是一个专为 Vue.js 应用程序开发的状态管理模式
## core concept
+ state: 定义状态值
+ getter: 状态值筛选的等处理
+ mutation：修改状态值（必须是同步函数），提交 mutation 是更改状态的唯一方法
+ Action：提交mutation（处理异步操作）
+ module：Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割


[vue-demo](vue-demo.egg123123.cn)

