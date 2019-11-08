---
title: Hello World
date: 2018/5/1
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
$ hexo server --port 5000
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)

# hexo
```bash
$ cnpm install hexo -g –-save
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

