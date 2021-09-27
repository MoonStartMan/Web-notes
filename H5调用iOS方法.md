# H5调用iOS方法

``` javascript

///	window.webkit.messageHandlers.name("方法名字").postMessage(参数);
///	name为方法名字
///	postMessage为传递的参数如果没有可以传空，不可以省略

///	例子
window.webkit.messageHandlers.closeWebview.postMessage("");

```