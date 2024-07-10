# Vue3腾讯地图获取当前位置信息

## 下载最新版 jQuery

## 在 index.html 中引入

``` javascript
<script src="./public/jquery-3.7.1.min.js"></script>
```

## 在腾讯地图开发者管理后台添加 key 配置白名单

## ajax完成请求

``` javascript
$.ajax({
    url: 'https://apis.map.qq.com/ws/location/v1/ip',
    type: 'GET',
    data: {
      key: '你的key',
      output:'jsonp' 
    },
    dataType:"jsonp",
    success: function (res) {
      console.log(res)
    },
    error: function (e) {
      console.log(e)
    },
  })
```

## 返回结果

``` json
{
	{
    "status": 0,
    "message": "Success",
    "request_id": "",
    "result": {
        "ip": "",
        "location": {
            "lat": "",
            "lng": ""
        },
        "ad_info": {
            "nation": "",
            "province": "",
            "city": "",
            "district": "",
            "adcode": "",
            "nation_code": ""
        }
    }
}
```