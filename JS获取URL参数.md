# JS获取URL参数

``` javascript

function getQueryVariable(variable)
{
	var query = window.location.search.substring(1);
	var vars = query.split("&")
	for (var i=0; i<vars.length; i++) {
		var pair = vars[i].split("=");
		if (pair[0] == variable) {
			return pair[1];
		}
	}
	return false
}

```

## 例子

``` javascript

var url = "http://www.runoob.com/index.php?id=1&image=awesome.jpg"
getQueryVariable("id")	///	返回 1
getQueryVariable("image") ///	返回awesome.jpg

```