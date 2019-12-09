# webpack 添加mp3文件

## 在webpack.common.js里面添加

``` JavaScript
{
  test: /\.(mp3)$/,
  use: [{
  	loader: 'url-loader',
  	options: {
  	//  图片输出的实际路径(相对于dist)
  		outputPath: 'audio',
  	//  当小于某KB时转为base64
  	limit: 0
  	}
  }]
},
```

## 安装copy-webpack-plugin

``` JavaScript
npm install copy-webpack-plugin --save-dev
```

## 配置copy-webpack-plugin

``` JavaScript
 new CopyWebpackPlugin([
 	{ from: './src/audio/', to: 'audio' }
 ])
```