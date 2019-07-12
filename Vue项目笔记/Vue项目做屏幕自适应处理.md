# Vue项目做屏幕自适应处理

### 1.安装felxible
```
npm install lib-flexible --save-dev
```

### 2.在main.js中引入
```
import 'lib-flexible'
```

### 3.在index.html文件中设置meta标签.
```
<meta name="viewport" content="width=device-width,initial-scale=1.0">
```

### 4.安装px2rem
```
npm install px2rem-loader -D
```

### 5.在utils.js中修改
```
const px2remLoader = {
    loader: 'px2rem-loader',
    options: {
    	//这个参数是通过PSD设计稿的宽度/10来计算，这里以1024为标准
        remUnit: 102.4
    }
}
```
修改 generateLoaders函数的loaders常量
```
const loaders = [cssLoader, px2remLoader]
```