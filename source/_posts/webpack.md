---
title: webpack
date: 2018/5/7
---

> 本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

# install
$ cnpm install webpack -g

### four core concepts
1. 入口(entry)：哪里作为关系图的起点
2. 输出(output)：属性告诉 webpack 在哪里输出它所创建的 bundles
3. loader：loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。
4. 插件(plugins)：用来处理各种各样的任务

### deploy
```js
//app/webpack.config.js 文件
var webpack=require('webpack');//webpack内置插件
 
module.exports = {
    entry: {index1: './src/js/entry.js', index2: './src/js/entry2.js'},//多入口
    output: {
        path : __dirname + '/out',
        publicPath: __dirname + '/out',//添加静态资源, 否则会出现路径错误
        filename : '[name].js',//这样就可以生成两个js文件, 名字分别为index1.js, 和index2.js
    },
    module: {//loader css jpg。。
        loaders: [
            { test: /\.css$/, loader: "style-loader!css-loader" },
            {test: /.(jpg|png|gif|svg)$/, use: ['url-loader?limit=8192&name=./[name].[ext]']}
        ]
    },
    plugins:[
        new webpack.BannerPlugin('菜鸟教程 webpack 实例')//实例化内置的 BannerPlugin 插件
    ]
};
```
[reference](https://blog.csdn.net/c_kite/article/details/71279853)

### command
$ webpack --progress --colors
当项目逐渐变大，webpack 的编译时间会变长，可以通过参数让编译的输出内容带有进度和颜色

$ webpack --progress --colors --watch
如果不想每次修改模块后都重新编译，那么可以启动监听模式。开启监听模式后，没有变化的模块会在编译后缓存到内存中，而不会每次都被重新编译，所以监听模式的整体速度是很快的。


# webpack-dev-server 开发服务
> 使用 webpack-dev-server 开发服务,这样我们就能通过 localhost:8080 启动一个 express 静态资源 web 服务器，并且会以监听模式自动运行 webpack，在浏览器打开 http://localhost:8080/ 或 http://localhost:8080/webpack-dev-server/ 可以浏览项目中的页面和编译后的资源输出，并且通过一个 socket.io 服务实时监听它们的变化并自动刷新页面。

## 安装
cnpm install webpack-dev-server -g

## 修改package.config.js
publicPath: 'http://localhost:8080/out',

## 修改html
```html
<!-- <script src="./out/index.js"></script> -->
<script src="http://localhost:8080/out/index.js"></script>
```

## 运行
webpack-dev-server --progress --colors
