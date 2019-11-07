# Vue+Webpack 搭建项目

## 项目初始化

1. 创建 package.json文件

```
npm init
```

2. 创建src目录作为项目目录

3. 创建webpack.config.js文件

``` JavaScript
const path = require('path')
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
    entry: path.join(__dirname, 'src/index.js'),
    output: {
        filename: 'bundle.js',
        path: path.join(__dirname, 'dist')
    },
    plugins: [
        new VueLoaderPlugin()
    ],
    module: {
        rules: [
            {
                test: /\.vue$/,
                use: [
                    'vue-loader'
                ]
            },
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.(gif|jpg|jpeg|png|svg)$/,
                use: [
                    {
                        loader: 'url-loader',
                        options: {
                            limit: 1024,
                            name: '[name].[ext]'
                        }
                    }
                ]
            }
        ]
    }
}
```

PS: 如果报错

```
his is probably not a problem with npm,there is likely additional logging output above

```
如果遇到以上错误

```
npm install webpack-cli --save-dev
```

```
webpack vue-loader was used without the corresponding plugin. Make sure to include VueLoaderPlugin
```

如果遇上错误,在webpack.config.js中加入

```
const VueLoaderPlugin = require('vue-loader/liu/plugin')
```

