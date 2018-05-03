---
title: Git
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

# quick start
>初始化（window+r cd 文件夹）
```bash
$ git init
```

>查看本地存储状态
```bash
$ git status
$ git status -s
```

>添加本地暂存（托管）文件
```bash
$ git add <file>
$ git add –all && git add .
```

>类似于node_modules这种性质的文件夹不应该被托管,添加一个本地git的忽略清单文件
在代码文件夹的根目录天剑一个.gitignore文件,该文件用于说明负略的文件有哪些

>设置name和email
```bash
$ git config --list //检查已有的配置信息
$ git config user.name  //检查指定环境变量设定
$ git config --global user.email 'you@email.com'  
$ git config --global user.name 'youname'
```

>提交被托管的代码变化到本地仓库
```bash
$ git commit -m ‘……’
```

>查看提交日志
```bash
$ git log
```

>回到指定版本
```bash
$ git reset --hard e377f60e28c8b84158
```

>对比差异
```bash
$ git diff
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

### branch
```bash
$ git branch //list branch
$ git branch gh-pages //create branch
$ git checkout gh-pages //checkout branch(using the branch)
$ git branch -d master //delete branch
```

移除本地分支：git remote rm origin
```bash
$ git pull
```

# hexo
```bash
$ cnpm install hexo -g –server
$ hexo init
$ hexo generate
$ hexo server 
$ hexo server -p 5000 //5000 port run
```

## hexo deploy

### themes 
```bash
$ cd d:blog
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
在blog中打开配置文件_config.yml，修改theme：next

### title author language 
blog/_config.yml文件修改 
title: egg
author: egg
language: zh-cns

### menu 
blog/themes/next/_config.yml文件修改
menu下增删修改菜单项
（注：千万不要在这设置中文，后面的值那是查找文件的地方！若你的站点运行在子目录中，请将链接前缀的 / 去掉）

### sidebar position
blog/themes/next/_config.yml文件修改
sidebar：
    &nbsp position：right

### code theme
blog/themes/next/_config.yml文件修改
highlight_theme，默认值为nomal。可以设置为night

> 其他主题也具有相似的配置方法（更多具体方法百度）



