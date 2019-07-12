# jQuery 动态创建元素绑定点击事件注意事项


## 实例

``` javascript
$('.btn').click(function(){  //code }) //普通绑定事件
$(document).on('click','.btn',function(){//code })  //on绑定事件
```

## 说明
	动态添加的HTML元素是在CSS，JS代码加载完成后再添加的HTML页面。在浏览器解析这些通过ajax请求到后台返回的数据,再根据返回的结果动态生成HTML页面时，这些绑定事件的标签元素还没有生成。而普通.click事件只能绑定静态元素。用on方法支持动态绑定元素。