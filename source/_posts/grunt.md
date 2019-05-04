---
title: grunt
date: 2018/5/9
categories:
- Project tools
---

> [node](/2018/05/08/node/) [nvm](http://www.jianshu.com/p/1aa925e3f0d6)

### npm
command|description
------|-----
$ npm init |创建package.json
$ npm install|安装package.json中的依赖模块
$ npm install packagename|安装最新模块
% npm install packagename 0.0.1|安装指定版模块
$ npm install packagename --save 或 -S|安装模块并把模块的版本信息保存到dependencies（生产环境依赖）中，即你的package.json文件的dependencies字段中；
$ npm install packagename --save-dev 或 -D|安装模块并把模块版本信息保存到devDependencies（开发环境依赖）中，即你的package.json文件的devDependencies字段中；
npm install packagename --save-optional 或 -O|安装模块并把把模块安装到optionalDependencies（可选环境依赖）中，即你的package.json文件的optionalDependencies字段中。


# grunt
> grunt是JavaScript世界的项目构建工具

## 为何要用构建工具
一句话：自动化。对于需要反复重复的任务，例如压缩（minification）、编译、单元测试、linting等，自动化工具可以减轻你的劳动，简化你的工作。当你在 Gruntfile 文件正确配置好了任务，任务运行器就会自动帮你或你的小组完成大部分无聊的工作。

## 为什么要使用Grunt？
Grunt生态系统非常庞大，并且一直在增长。由于拥有数量庞大的插件可供选择，因此，你可以利用Grunt自动完成任何事，并且花费最少的代价。如果找不到你所需要的插件，那就自己动手创造一个Grunt插件，然后将其发布到npm上吧。先看看入门文档吧。

## 安装grunt
$ npm install grunt -save-dev

使用中国节点，淘宝镜像来代替npm的国外节点
$ npm install -g cnpm --registry=https://registry.npm.taobao.org

然后
$ cnpm install grunt --save-dev

安装grunt-cli工具 全局安装
$ cnpm install grunt-cli -g


### grunt-spritesmith
+ $ cnpm install grunt-spritesmith --save-dev
+ 配置grunfile.js
+ 运行grunt sprite

### grunt-contrib-cssmin
+ $ npm install grunt-contrib-cssmin --save-dev
+ 配置grunfile.js
+ 运行grunt cssmin

### grunt-contrib-cssmin
+ $ npm install grunt-contrib-cssmin --save-dev

# package.json
```js
{
  "name": "gruntproject",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "grunt": "^1.0.2",
    "grunt-contrib-concat": "^1.0.1",
    "grunt-contrib-cssmin": "^2.2.1",
    "grunt-contrib-htmlmin": "^2.4.0",
    "grunt-contrib-jshint": "^1.1.0",
    "grunt-contrib-less": "^1.4.1",
    "grunt-contrib-uglify": "^3.3.0",
    "grunt-contrib-watch": "^1.0.1",
    "grunt-spritesmith": "^6.6.0"
  }
}
```

# gruntfile.js
```js
module.exports = function(grunt) {

  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    sprite:{
      all: {
        src: './public/imgs/indexp*.png',
        dest: './build/imgs/spritesheet.png',
        destCss: './build/css/sprites.css'
      }
    },
    htmlmin: {
     target: {
        files: [{
          expand: true,
          cwd: './public/',
          src: ['*.html'],
          dest: './build/',
          ext: '.html'
        }]
      }
    },
    less: {
      main: {
          expand: true,
          src: ['./public/css/*.less'],
          dest: './',//css同路径下
          ext: '.css'
      },
      dev: {
          options: {
              compress: true,
              yuicompress:false
          }
      }
    },
    cssmin: {
      target: {
        files: [{
          expand: true,
          cwd: './public/css/',
          src: ['*.css', '!*.min.css'],
          dest: './build/css/',
          ext: '.min.css'
        }]
      }
    },
    jshint: {
      src:["./public/js/*.js",'!./public/js/jquery-3.2.1.js']
    },
    uglify: {
      my_target: {
        files: [{
          expand: true,
          cwd: './public/js/',
          src: ['*.js', '!*.min.js','!jquery-3.2.1.js'],
          dest: './build/js/',
          ext: '.min.js'
        }]
      }
    },
    concat: {
      dist: {
        src: ['./public/js/*.js'],
        dest: './public/global.js',
      },
    },
    watch: {
      scripts: {        
        files: ['*.js', '!*.min.js','!jquery-3.2.1.js'],
        tasks: ['jshint']
      },
      less: {
        files: ['./css/*.less'],
        tasks: ['less']
      }
    }
  });

  grunt.loadNpmTasks('grunt-spritesmith');
  grunt.loadNpmTasks('grunt-contrib-htmlmin');
  grunt.loadNpmTasks('grunt-contrib-cssmin');
  grunt.loadNpmTasks('grunt-contrib-less');
  grunt.loadNpmTasks('grunt-contrib-concat');
  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-contrib-uglify');
  grunt.loadNpmTasks('grunt-contrib-watch');

  grunt.registerTask('min',['cssmin','uglify']);//grunt min
  grunt.registerTask('default');

};
```

ctrl+c 关闭执行的功能

