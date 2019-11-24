---
title: 有纪-Problems encountered and Solutions
date: 2019-11-24 10:56:39
tags:
---
## 项目框架
基于 `react-express-webpack` 的项目框架进行开发
## 搭建脚手架以及文件打包
### webpack : 无法将“webpack”项识别为 cmdlet、函数、脚本文件或可运行程序的名称
需全局安装 webpack ，`npm install -g webpack`，把node_global加入到环境变量。

### 使用webpack构建本地服务器
`npm install --save-dev webpack-dev-server`
浏览器监听代码的修改，并自动刷新显示修改后的结果
在终端中输入`npm run server`即可在本地的8080端口查看结果

### 关于webpack中的Babel
Babel是一个编译JavaScript的平台
* 可以使用最新的JavaScript代码（ES6,ES7...），而不管新标准是否被当前使用的浏览器完全支持；
* 可以使用基于JavaScript拓展的语言，比如React中的JSX；
`npm install --save-dev babel-core babel-loader babel-preset-env babel-preset-react` 安装多个依赖模块，模块之间用空格隔开

配置babel，可以使用es6和jsx语法
```js
module: {
    rules: [
        {
            test: /(\.jsx|\.js)$/,
            use: {
                loader: "babel-loader",
                options: {
                    presets: [
                        "env", "react"
                    ]
                }
            },
            exclude: /node_modules/
        }
    ]
}
```
### 安装react 和 react-dom
`npm install --save react react-dom`












***
## 项目目录结构
`app`文件夹存放原始数据和js模块，`public`文件夹用来存放供浏览器读取的文件（包括使用webpack打包生成的js文件和index.html）