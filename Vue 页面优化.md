## Vue项目的性能优化

### gzip压缩
``` 
#开启gzip
gzip on;
#启用gzip压缩的最小文件,小于设置的文件将不会压缩
gzip_min_length 1k;
# gzip压缩级别 1-10,数字越大压缩的越好,也越占用CPU时间.
gzip_comp_level 2;
# 进行压缩的文件类型。javascript有多种形式。其中的值可以在mime.types文件中找到。
gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
# 是否在http header 中添加 Vary:Accept-Encoding,建议开启
gzip_vary on
# 禁用IE 6 gzip
gzip_disable "MSIE [1-6]";
```

### 服务器缓存
#### 为了提高服务器获取数据的速度,nginx缓存着静态资源是非常必要的。如果是测试服务器对html应该不设置缓存,而js等静态资源环境因为文件尾部会加上一个hash值,这可以实现缓存的控制。
```
location ~* ^.+\.(ico|gif|jpg|jpeg|png)$ {
    access_log	off;
    expirse	30d;
} 
location ~* ^.+\.(css|js|txt|xnk|swf|wav)$ {
    access_log	off;
    expirse	24h;
}
location ~* ^.+\.(html|htm) ${
    expirse	1h;
}
```
### 浏览器缓存
#### 浏览器缓存是通过html头文件中的meta来控制。http-equiv是一个在专门针对http的头文件,可以向浏览器传回一些有用的消息。与之对应的content,是各个参数的变量值。
#### HTTP 1.0
##### 在HTTP1.0通过Pragma控制页面缓存,可以设置为Pragma或者no-cache。在不让浏览器或中间缓存服务器缓存页面的情况下,通过设置的值为no-cahe,不过这个值不这么保险,通常还加上Expires设置为0来达到目的。Expires可以用于设定网页的到期时间。一旦网页到期,必须到服务器上重新传输获取新的页面信息。PS:内容必须使用GMT的时间格式。
```
<meta http-equiv="Pragma" content="no-cahe">
<meta http-equiv="Expires" content="0">
```
#### HTTP1.1
##### 在HTTP1.1中通过-Cache-Control控制页面缓存,可以设置为no-cache、private、no-store、max-age或must-revalidate等,默认为private。
+ public:浏览器和缓存服务器都可以缓存页面信息
+ private:对于单个用户的整个或部分响应消息,不能被共享缓存处理。这允许服务器仅仅描述当用户的部分响应消息,此响应消息对于其他用户的请求无效
+ no-che:浏览器和缓存服务器都不应该缓存页面信息
+ no-store:请求和响应的信息都不应该被存储在对方的磁盘中,不适用缓存
+ must-revalidate:对于客户机的每次请求,代理服务器必须想服务器验证缓存是否过时
+ max-age:客户机可以接收生存期不大于指定时间(以秒为单位)的响应
+ min-fresh:客户机可以接收响应式时间小于当前时间加上指定时间的响应

#### Last-Modified和Etags
##### Last-Modified服务器端文件响应头,描述最后修改时间。当浏览器再次进行请求时,会向服务器传送If-Modified-Since报头,询问时间点之后资源是否被修改过,从而区分200和304的请求状态码,304则选择浏览器缓存。
##### Etags不同的是,ETag是根据实体内容生成一段hash字符段,是标识资源的状态。它由服务端产生来判断文件是否更新。

#### JS分包
##### 因为Vue的脚手架搭建的项目,webpack的配置当中就包含了压缩js,css,html的压缩。所以当我们的单页面越做越大的情况下,首要的一步就是分包
##### 两种分包的方法:
+ external 把包排除,使用cdn资源
+ dll 打包

##### **vue,vuex和vue-router**
##### 在webpack配置文件中external设置,把这三个场用包排除这个操作,主要是把这三个包从vendor.js分开
##### 最后当然需要在html标签上添加额外cdn的link或者script.
#### DLL打包
##### 这种打包方式专门引用webpack官方的DllPlugin和DllReferencePlugin。DllPlugin会生成一个dll包的代码指纹manifest,管理额外的打包。而在项目生成的的过程中,DllReferencePlugin会参考manifest的内容去打包。额外生成的js文件应该被放置在vue项目的文件当中的static文件底下,以便于代码部署。
#### 预加载
##### 预加载技术(prefetch)是在用户需要前我们就将所属的资源加载完毕,不是所有的浏览器都支持,主要是Chrome浏览器。
##### 由于域名转换成为IP的过程是非常耗时的一个过程,DNS prefetch可以减少这部分的时间。
```
<meta http-equiv='x-dns-prefetch-control' content='on'>
<link rel='dns-prefetch' href='http://g-ecx.images-amazon.com'>
<link rel='dns-prefetch' href='http://z-ecx.images-amazon.com'>
<link rel='dns-prefetch' href='http://ecx.images-amazon.com'>
<link rel='dns-prefetch' href='http://completion.amazon.com'>
<link rel='dns-prefetch' href='http://fls-na.amazon.com'>

```
##### 预加载也可以对某个静态资源起到专门的作用
```
<link ref='subresource' href='libs.js'>
```
##### 预渲染(pre-rendering)是这个页面会提前加载好用户即将访问的下一个页面。
```
<link ref='prerender' href='http://www.pagetoprerender.com'>
```
#### vue组件kepp-alive
##### 如果你做用一个大型web的spa的时候,你有很多router,对应的是很多个页面。在页面的快速切换中,为了保证页面加载的效率,除了缓存机制以外,vue的keep-alive组件可以帮的上忙。它会把组件保存在浏览器内存当中,方便你快速切换。
##### 百度的lavas项目中就在vue-router当中使用keep-alive组件,用它包裹着router-view。使用keep-alive的组件内的数据将会保留,"是否需要重新同步数据"可以在vue-router的钩子中路由所带的参数执行判断。
#### Promise请求
##### es6的其中一个特性就是原生支持promise。
##### promise的特点在于:
+ 减少回调函数
+ 串并行处理
+ 代码的优雅

##### 这里特别讲一下,ES6在性能优化上可以使用promise或者async/await去压缩请求时间。在过去,很多jquery的页面在调用接口请求都是一个接口等另一个接口,串行执行所有请求,最后在完成最后的回调函数,如此类推。这样的写法会直接导致"回调地狱"。即使你使用vue-resource,我也review到非常多的"回调地狱"的情况。为了从根本上解决这个问题并提高开发效率，我建议先使用promise。(async/await不急着投入使用),考虑到很多同事还在高效地开发业务代码。
##### 现在的vue-resource已经支持promise的写法，为了更好地让技术向后发展，我建议将pagekit/vue-resource替换称为mzabriskie/axios和webmodules/jsonp。axios是可以同时满足服务端和浏览器端，同构的写法有助于以后将技术栈往SSR（服务端渲染）发展。jsonp这个库则是为了兼容jsonp的请求需要，需要对它进行了promise的封装。
```
export function getJsonp(urlHost, key, data, _params) {
  return new Promise((resolve, reject) => {
    let url = urlHost + key;
    if (data) url += `?${querystring.stringify({ ...data, temp: new Date().getTime() })}`;
    const params = _params || { timeout: 15000 };
    if (!params.timeout) params.timeout = 15000;
    jsonp(url, params, (err, res) => {
      if (err) {
        reject(err);
      } else {
        resolve(res);
      }
    });
  });
}
```
##### Promise的使用需要避免以下的写法,
```
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```
##### 尽量使用链式写法,
```
promise.then(function(value) {
  // step1
}).then(function(value){
  // step2
}).catch(function(value){
  // failure
})
```
##### 并行的操作主要是Promise.all()，它可以将Promise操作的数组并行执行完成然后在进行串行的操作。Promise.race()则是返回并行请求中最先返回的请求的那个结果。它们的使用可以有效地压缩数据获取的时间。

