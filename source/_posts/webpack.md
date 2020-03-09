---
title: webpack
date: 2018/5/7
categories:
- Project tools
---

> 本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

# repuire and import
+ let { stat, exists, readFile } = require('fs'); 
整体加载fs模块（即加载fs所有方法），生成一个对象"_fs"，然后再从这个对象上读取三个方法，这叫“运行时加载”，因为只有运行时才能得到这个对象，不能在编译时做到静态化。
+ import { stat, exists, readFile } from 'fs';
从fs加载“stat, exists, readFile” 三个方法，其他方法不加载，
tips: import命令具有提升效果，会提升到整个模块的头部，首先执行。（是在编译阶段执行的）因为import是静态执行的，不能使用表达式和变量，即在运行时才能拿到结果的语法结构（e.g. if...else...）所以不能实现按需加载

# export and export default
export时，使用import导入，都需要知道模块中所要加载的变量名或函数名，用户可能不想阅读源码，只想直接使用接口，就可以用export default命令
tips：export default 一般用于导出一个function或class（如：react 的组件与reducer)

# import()
解决import按需加载问题
```js
if (condition) {
  import('moduleA').then(...);
} else {
  import('moduleB').then(...);
}
```

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
const webpack = require('webpack');
const {DefinePlugin, HashedModuleIdsPlugin} = webpack;//webpack内置插件
const {version} = require('../package.json');
const options = {env: 'dev'}
 
module.exports = {
    // target: 'web', //构建目标，默认web，编译为类浏览器环境里可用
    mode: options.env === 'dev' ? 'development' : 'production',// 打包模式
    entry: {index1: './src/js/entry.js', index2: './src/js/entry2.js'},//多入口
    output: {
        path : __dirname + '/out',
        publicPath: __dirname + '/out',//添加静态资源, 否则会出现路径错误
        filename : '[name].js',//这样就可以生成两个js文件, 名字分别为index1.js, 和index2.js
        chunkFilename: options.env === 'dev' ? `chunks/[name].js?v=[chunkhash:6]` : `s/[name].js?v=[chunkhash:6]_${v.localVersion}`
    },
    module: {//loader css jpg。。
        loaders: [
            { test: /\.css$/, loader: "style-loader!css-loader" },
            {test: /.(jpg|png|gif|svg)$/, use: ['url-loader?limit=8192&name=./[name].[ext]']}
        ]
    },
    plugins:[
        // 项目中的 __VERSION__ 替换为 version 值
        new DefinePlugin({
            "__VERSION__": JSON.stringify(version)
        })
    ],
    resolve:{
        // 告诉 webpack 解析模块时应该搜索的目录(默认["node_modules"])
        modules: ["node_modules"， "custom_modules"],
        // 解析目录时要使用的文件名。构建目标 target： “web” 时默认：mainFiles: ["index"]
        mainFiles: ["index"],
        //配置别名，在项目中可缩减引用路径
        alias: {
            '@': resolve('src/components'),
            'api': resolve('src/api'),
            'assets': resolve('src/assets')
        }
    }
};
```
[reference](https://blog.csdn.net/c_kite/article/details/71279853)

### command
$ webpack --progress --colors
当项目逐渐变大，webpack 的编译时间会变长，可以通过参数让编译的输出内容带有进度和颜色

$ webpack --progress --colors --watch
如果不想每次修改模块后都重新编译，那么可以启动监听模式。开启监听模式后，没有变化的模块会在编译后缓存到内存中，而不会每次都被重新编译，所以监听模式的整体速度是很快的。

1. 配置相关的参数
--env：设置环境变量
--config：配置文件路径   如：--config webpack.dist.config.js
--mode：开发模式   如：--mode production or --mode developement

2. 输出相关的参数
--output-path：输出文件路径
--output-filename：输出文件名按照自己的格式输出
--output-source-map-filename：映射文件名，文件打包后与源文件有一个映射关系，可以通过map找到源文件

3. Debug参数：
--debug:  打开debug模式
--progress: 打印编译的进度
--devtool: 定义source map类型
--display-error-details： 显示错误详情

4. Module 参数
--module-bind： 绑定一个拓展程序 如：--module-bind js=babel-loader

5. watch参数
--watch：监听文件变化

6. Optimize 参数
--optimize-max-chunks：设置代码块最大数量
--optimize-max-chunks 10
--optimize-min-chunk-size：设置代码块最小值
--optimize-min-chunk-size 10000
--optimize-minimize：压缩js文件

7. Stats 参数
--display： 显示打包信息，将具体信息可参考这里
--color, --colors：console里面显示颜色

8. 高级参数
--bail:  如果编译过程一有error，立马停止编译
--hot： 热替换，在config文件中也可配置
--provide：提供一些模块，做全局使用 如：--provide jQuery=jquery
--profile: 提供每一步编译的具体时间

[more](https://webpack.js.org/api/cli/#src/components/Sidebar/Sidebar.jsx)


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

“inline”选项会为入口页面添加“热加载”功能，
“hot”选项则开启“热替换（Hot Module Reloading）”，即尝试重新加载组件改变的部分（而不是重新加载整个页面）。
如果两个参数都传入，当资源改变时，webpack-dev-server将会先尝试HRM（即热替换），如果失败则重新加载整个入口页面。
