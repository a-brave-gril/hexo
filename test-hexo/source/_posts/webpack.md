---

title:  webpack小结
date:  #时间，一般不用改
categories:  前端笔记-git篇
tags:  [webpack,打包,webpack配置] #标签，格式可以是[Hexo,总结]，中间用英文逗号分开
keywords:  [webpack入门,webpack配置代码] #文章关键词，多个关键词用英文逗号隔开

---
##     webpack 是一个现代 JavaScript 应用程序的模块打包器(module bundler)。
##     webpack与其他打包工具的比较
       1.      webpack有两种加载方式：同步和异步。异步主要是为了按需加载，提高前端性能
       2.      webpack可以通过加载器可以将其他类型的资源转换为JS输出。
       3.      webpack有强大的插件系统，当webpack内置的功能不能满足我们的构建需求时，我们可以通过使用插件来提高工作效率。
* * * *
##     webpack的注意事项
       1.  在使用webpack之前，一定要确定使用的是最新的node.js版本，不然在打包的时候会发生很多错误。
       2.  webpack1与webpack2使用的时候还是有所差异的，所以要先确定你使用的版本号。
* * * *
##   安装webpack
       1.  首先新建一个文件夹并执行 npm init(初始化)
       2.  下载webpack npm install --save-dev webpack
       3.  下载您需要的插件以及loader （比如：npm install --save-dev css-loader--save-dev html-webpack-plugin）
       4.  新建webpack.config.js文件，并写入相应配置项，执行 webpack指令就可以完成打包。
       5.  webpack启动本地服务。推荐这篇文章：http://www.jianshu.com/p/42e11515c10f
       6.  注意：如果在下载的时候出现错误，您可以试试 cnpm install --save-dev w在国内下载的快，
               但是npm要从国外下载会很慢。但是cnpm更新的可能没有npm及时
* * * *
##     webpack 部分指令
       1.      npm install --save-dev webpack（安装）
       2.      npm install --save-dev style-loader(下载style-loader  style-load是将打包后的样式插入html的head中)
       3.      npm install --save-dev css-loader(下载css-loader)
       4.      npm install --save-dev html-webpack-plugin(下载html-webpack-plug插件，
                 html-webpack-plugin主要是自动生成打包后的html文件，并自动引用打包文件)
       5.      npm install --save-dev extract-text-webpack-plugin(下载extract-tt-webpack-plugin插件，
                 extract-text-webpack-plugin主要是将css打包当单独的一个css样式中)
       6.      npm run server(启动本地服务器)
       7.      npm install --save-dev sass-loader (打包scss文件)
* * * *
##     webpack.config.js 配置代码
    ···
               var HtmlWebpackPlugin = require('html-webpack-plugin'); // 打包生成html文件
               const ExtractTextPlugin = require("extract-text-webpack-plugin"); // 将css文件单独打包到一个文件中
               const path = require('path');

               module.exports = {
                       entry: './src/main.js',//唯一的入口文件。
                       devtool: 'inline-source-map',//调试时使用，可以定位到报错的文件以及位置
                       output: {//出口文件 可以有多个
                               filename: 'bundle.js', //打包的文件名
                               path: path.resolve(__dirname, 'dist') // 打包文件路径
                       },
                       devServer: {
                               contentBase: "./dist",//本地服务器所加载的页面所在的目录
                               historyApiFallback: true,//不跳转
                               inline: true//实时刷新
                       },
                       module: {
                               rules: [ //使用loader
                                       {
                                               test: /\.scss$/, //编译.scss文件
                                               use: ExtractTextPlugin.extract({
                                                 fallback: "style-loader",
                                                 use: ["css-loader","sass-loader"]
                                               })
                                       }
                               ]
                       },
                       plugins: [ //使用插件
                               new HtmlWebpackPlugin(),
                               new ExtractTextPlugin("styles.css")
                       ]
               };
       ···
