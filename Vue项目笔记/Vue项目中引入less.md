# Vue项目中引入less

### 1.安装less依赖
```
npm install less less-loader --save-dev
```

### 2.修改webpack.config.js文件，配置loader加载依赖
```
{
    test:/\.less$/,
    loader: "style-loader!css-loader!less-loader"
}
```

### 3.在style标签里面加入lang=less
```
<style lang="less"></style>
```