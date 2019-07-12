## AJAX上传图片和内容
#### JS部分代码
```
var img = document.getElementById("img");
    for(let i=0 ; i<img.files.length; i ++) {
        var file = img;
        if(img.files[i]) {
            formData.append("file", file.files[i]);
        }
    }
    formData.append("type",select);
    formData.append("title",topic);
    formData.append("author",author);
    formData.append("massage",message);
    formData.append("address",address),
    formData.append("organizer",organizer);
    formData.append("time",time);
```

+ 类似于formData.append(‘barterCategoryid', _self.goodstype); 是一种键值对的形式保存数据，而formData.append(“file”, file.files[0], file.files[0].name); 第一个参数为服务端接收的参数名，第二个为文件对象，第三参数为文件名称，这样可以将多个文件添加为数组的形式给服务器。

#### AJAX部分代码:
```
$.ajax({
    contentType: "application/json;charset=utf-8",
    url: URL请求地址
    type: "POST",
    data: formData,
    processData: false,
    contentType: false,
    success: function() {
    alert("上传成功!");
    },
    error:function(){
    alert("上传失败!");
    }
});
参数解释：
processData：要求为Boolean类型的参数，默认为true。默认情况下，发送的数据将被转换为对象（从技术角度来讲并非字符串）以配合默认内容类 型"application/x-www-form-urlencoded"。如果要发送DOM树信息或者其他不希望转换的信息，请设置为false。
contentType:要求为String类型的参数，当发送信息至服务器时，内容编码类型默认为"application/x-www-form-urlencoded"。该默认值适合大多数应用场合。
```