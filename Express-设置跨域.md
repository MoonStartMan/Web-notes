# Express-解决跨域及设置ip访问

## Express-解决跨域

``` javascript

app.all('*', function (req, res, next) {
    res.header('Access-Control-Allow-Origin', '*');
    //  Access-Control-Allow-Header, 可根据浏览器的F12查看，把对应的粘贴在这里就行
    res.header('Access-Control-Allow-Origin', 'Content-Type');
    res.header('Access-Control-Allow-Mehods', '*')
    res.header('Content-Type', 'application/json;charset=utf-8');
    next();
});

```

## 设置ip访问

``` javascript

const port = 3000 //指定端口

app.listen(port,'172.28.6.238')

```