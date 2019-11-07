# 利用webpack4.x创建react项目

## 配置webpack
1.运行 npm init -y快速初始化项目
2.在运行目录创建src源代码目录和dist产品目录
3.在src目录下创建index.html
4.使用npm安装webpack,运行`npm i webpack webpack-cli -D`
5.注意：webpack4.x提供了约定大于配置的概念；目的是为了尽量减少配置文件的体积；
	+ 默认约定了：
	+ 打包的入口是`src`->`index.js`
	+ 打包的输出文件是`dist`->`main.js`
	+ 4.x中新增了`mode`选项（为必选项），可选的值为：`development`和`production`

## 安装react
```
npm install react react-dom --save-dev
```

## 使用react
在index.js中输入
```
import React from 'react';
import ReactDOM from 'react-dom';
```

## 配置webpack-dev-server、html-webpack-plugin、babel
安装 webpack-dev-server、html-webpack-plugin
```
npm install webpack-dev-server --save-dev
npm install html-webpack-plugin --save-dev
```

安装 babel 插件
```
npm install babel-core babel-loader babel-plugin-transform-runtime --save-dev
npm install babel-preset-env babel-preset-stage-0 --save-dev
npm install babel-preset-react
```

添加webpack.config.js
``` webpack.config.js
//  向外暴露一个打包的配置对象;因为webpack 是基于node构建的； 所以webpack支持所有node API和语法
//  webpack 默认只能打包处理 .js后缀名类型的文件; 像.png .vue 无法主动处理，所以要配置第三方的loader;
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');   //  导入在内存中自动生成 index 页面的插件

//  创建一个插件的实例对象
const htmlPlugin = new HtmlWebpackPlugin({
    template: path.join(__dirname,'./src/index.html'),//    源文件
    filename:'index.html',  //  生成内存首页的名称
})

module.exports = {
    mode: 'development', // development production
    //  在 webpack4.x中，有一个很大的特性，就是约定大于配置 约定，默认的打包入口路径是 src -> index.js
    // entry: {
    //     app: './src/index.js'
    // },
    // output: {
    //     filename: 'bundle.js',
    //     path: path.resolve(__dirname,'./dist')
    // },
    plugins: [
        htmlPlugin
    ],
    module: {   //  所有第三方 模板的配置规则
        rules: [  //    第三方匹配规则
            {
                test: /\.js|jsx$/,
                use: 'babel-loader',
                exclude: /node_modules/, //千万别忘记exclude排除项
            }
        ]
    },
    resolve: {
        extensions: ['.js', '.jsx', '.json'],   //  表示，这几个文件的后缀名，可以省略不写
        alias: {//  表示别名
            '@' :path.join(__dirname, './src')   //  这样, @ 就表示项目根目录中 src 这一层路径
        }
    }
}
```

添加.babelrc配置文件
``` 
{
    "presets": [
        "env",
        "stage-0",
        "react"
    ],
    "plugins": [
        "transform-runtime"
    ]
}
```

## 修改package.json文件
``` json
"scripts": {
	"dev": "webpack-dev-server --open --port 3000 --hot"
}
```