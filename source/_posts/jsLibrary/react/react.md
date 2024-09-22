---
title: react
date: 2022/5/10
categories:
- jsLibrary
---

### react组件扽渲染流程
1. 执行组件的render方法
2. 执行render方法里的React.createElement方法创建虚拟DOM，从而得到虚拟DOM树
3. 根据虚拟DOM树在界面上生成真实DOM

### react组件的更新流程
1. 组件的props/state发生改变
2. render方法重新执行
3. 利用React.createElement方法重新生成新虚拟DOM树
4. 新旧虚拟DOM树通过“diff 算法”进行比较
5. 每发现一个不同就生成一个mutation去记录这个不同
6. 根据mutation更新真实DOM

### DIFF 算法
+ 只会同层比较
+ 默认在同层比较时，只会进行同位置比较
  + 在比较的是相同类型元素时，就只记录变化
  + 在比较的是不同类型元素时，就直接使用新的元素即新元素的子孙元素（即直接从这个元素开始的分支）

