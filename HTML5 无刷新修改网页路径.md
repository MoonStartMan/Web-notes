# HTML5 无刷新修改网页路径

通过pushState（）传值修改

``` javascript
var url =window.location.search.substring(6);
if(!url) {
    window.history.pushState({},0,"?type=index");
}
```