---
title: Git
date: 2018/5/3
---

what is git?
> 是一个源代码管理工具
在一个项目中，凡是由开发人员编写的都算源代码
源代码为什么需要管理？
让源代码可以被追溯，主要记录每次变更了什么，谁主导的这次变化
认为管理和维护比较麻烦
Git是Linux之父当年为了维护Linux的源代码编写的一个工具
Git之前都用什么？ svn vss tfs……

### Git 与 SVN 区别
1. GIT是分布式的，SVN不是：这是GIT和其它非分布式的版本控制系统，例如SVN，CVS等，最核心的区别。
2. GIT把内容按元数据方式存储，而SVN是按文件：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn,.cvs等的文件夹里。
3. GIT分支和SVN的分支不同：分支在SVN中一点不特别，就是版本库中的另外的一个目录。
4. GIT没有一个全局的版本号，而SVN有：目前为止这是跟SVN相比GIT缺少的最大的一个特征。
5. GIT的内容完整性要优于SVN：GIT的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。

# 安装git
download:http://git-scm.com/downloads
windows安装后配置环境变量

## quick start
1. 初始化（window+r cd 文件夹）
```bash
$ git init
```

2. 查看本地存储状态
```bash
$ git status
$ git status -s
```

3. 添加本地暂存（托管）文件
```bash
$ git add <file>
$ git add –all && git add .
```

4. 提交被托管的代码变化到本地仓库
```bash
$ git commit -m ‘……’
```

5. 显示最近一次提交文件中对每一行进行修改的相关信息（修改人，时间等）
```bash
$ git blame <file>
$ git blame -L 12,22 simplegit.rb //只显示12-22行
```

6. 查看提交日志
```bash
$ git log
```

7. 移除本地分支
```bash
$ git remote rm origin
```

8. 对比差异
```bash
$ git diff //不加参数即默认比较工作区与暂存区
$ git diff --cached  [<path>...] //比较暂存区与最新本地版本库
$ git diff HEAD [<path>...] //比较工作区与最新本地版本库　　　　　
```

>类似于node_modules这种性质的文件夹不应该被托管,添加一个本地git的忽略清单文件
在代码文件夹的根目录添加一个.gitignore文件,该文件用于说明负略的文件有哪些

## 恢复（回退）
1. 将还未添加到暂存区中的文件恢复到修改前
```bash
git checkout -- <file>
```

2. 将已经添加到暂存区中但还未提交的文件恢复到添加至暂存区之前
```bash
git reset HEAD <file>...
```

3. 回到指定版本
```bash
$ git reset --hard e377f60e28c8b84158   
git push -f     //因为我们本地库HEAD指向的版本比远程库的要旧-f强制推上去

$ git reset --soft e377f60e28c8b84158   //源节点和reset节点的差异放在暂存区

$ git reset --mixed e377f60e28c8b84158  //源节点和reset节点的差异和原暂存区中的内容都放在工作区
$ git reset  e377f60e28c8b84158   //默认参数 --mixed
```

4. 回滚指定版本(将提交的某个版本反做一遍)
```
$ git revert -n 8b89621019c9adc6fc4d242cd41daeb13aeb9861
```

## branch
```bash
$ git branch //list branch
$ git branch gh-pages //create branch
$ git checkout gh-pages //checkout branch(using the branch)
$ git branch -d master //delete branch
$ git merge <brench> //merge branch
$ git checkout feature <file>... //Partial merger
```

# 储藏 stash
> 储藏自上次提交之后的工作
command | description
--------|------------
git stash pop | 应用并删除最新储藏的工作
git stash pop --index | 回到最新储藏前的工作位置（以前做的add也恢复）
git stash apply stash@{2} | 应用储藏的对应工作（并未删除）
git stash apply stash@{2} --index | 应用储藏的对应工作（并未删除）（以前做的add也恢复）
git stash show -p stash@{0} | 取消应用的储藏
git stash drop stash@{0} | 删除指定的储藏
git clear | 清空所有的储藏的工作


# git config
> git 配置文件分为三级，
local仓库级在当前项目的 .get/config（git init 时会创建)
global用户级在用户目录下的 ~.gitconfig（如C:\Users\Administrator\.gitconfig)
system系统级在安装木下（C:\Program Files\Git\mingw64\etc\gitconfig)

##　Configuration item　description

item|description
-----|----------
user.name|用户名
user.email|邮箱
core.editor| 默认编辑器
merge.tool | 解决合并时冲突的工具
alia.xx | 设置命令的别名 （git config --global alias.st status） st 就等于status
color.branch color.diff color.interactive color.status | 颜色配置 （git config --global color.diff.meta "blue black bold"）这样会将diff的输出以蓝色字体，黑色背景，粗体显示。


```bash
$ git config --list //查看所有的配置信息
$ git config --global --list //只查看用户级的配置信息
$ git config user.name  //检查指定环境变量设定
$ git config --global user.email 'you@email.com'  
$ git config --global user.name 'youname'
$ git config --add cat.name tom //添加配置项
$ git config --get cat.name //等同于git config cat.name
$ git config --unset cat.name //删除配置项
$ git help log //获取对应指令的手册页--帮助
```

### GitHub是什么？
> 只是一个网站
同行交友社区，人群都是程序员
https://GitHub.com/
提出概念 社交化编程
他是git的服务提供商，提供了free仓库–前提是开源

注册
建开源仓库
```bash
$ echo “# egg” >> README.md
$ git init
$ git status
$ git add README.md
$ git commit -m “first commit”
$ git remote add origin https://github.com/egg123456/egg.git
$ git push -u origin master
```

# 远程库
```bash
$ git reomte add origin https://github.com/egg123456/egg.git 
$ git remote rm origin      //移除远程库
$ git remote rename origin origin_blog      //重命名远程库
$ git remote show origin_blog     //远程库信息
$ git remote set-url origin_blog https://github.com/egg123456/blog.git    //修改本地仓库指向的远程库
```



