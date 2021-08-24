# express解决本地接口跨域问题

在index.js文件中添加以下代码

``` javascript

app.all('*', function (req, res, next) {
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Headers', 'X-Requested-With');
    res.header('Access-Control-Allow-Mehods', '*');
    res.header('Content-Type', 'application/json;charset=utf-8');
    next();
});

```

即可解决跨域错误。