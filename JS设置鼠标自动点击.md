## JS自定义事件的定义和触发(createEvent, dispatchEvent)
#### 相关代码:
```
<script type="text/javascript">
// 两秒后模拟点击
setTimeout(function() {
    // IE
    if(document.all) {
        document.getElementById("clickMe").click();
    }
    // 其它浏览器
    else {
        var e = document.createEvent("MouseEvents");
        e.initEvent("click", true, true);
        document.getElementById("clickMe").dispatchEvent(e);
    }
}, 2000);
</script>
```

#### 在JavaScript前端开发中，我们经常调用click、mouseup等基本事件。有的时候，为了满足特定功能的要求，我们需要自定义事件，这就要说到自定义事件的运作机制。

#### 由于浏览器兼容性问题，针对标准浏览器和IE6/7等浏览器。
+ 1. 对于标准浏览器，其提供了可供元素触发的方法：element.dispatchEvent(). 使用该方法之前需要进行创建和初始化。因此，总结说来就是：

```
document.createEvent()
event.initEvent()
element.dispatchEvent()
```

+ 2. 例子：

```
$(dom).addEvent("alert", function() {
    alert("ABC");
});

// 创建
var evt = document.createEvent("HTMLEvents");
// 初始化，事件类型，是否冒泡，是否阻止浏览器的默认行为
evt.initEvent("alert", false, false);

// 触发
dom.dispatchEvent(evt);
```

##### createEvent()方法返回新创建的Event对象，支持一个参数，表示事件类型，具体见下表：
|     参数     |    事件接口    |     初始化方法     |
|-------------|:-------------:|-----------------:|
| HTMLEvents  |   HTMLEvent   |    initEvent()   |
| MouseEvents |   MouseEvent  | initMouseEvent() |
|  UIEvents   |    UIEvent    |    initUIEvent() |

##### initEvent()方法用于初始化通过DocumentEvent接口创建的Event的值。支持三个参数：initEvent(eventName, canBubble, preventDefault). 分别表示事件名称，是否可以冒泡，是否阻止事件的默认操作。
##### dispatchEvent()就是触发执行了，dom.dispatchEvent(eventObject), 参数eventObject表示事件对象，是createEvent()方法返回的创建的Event对象。

#### 2. 对于IE浏览器，由于向下很多版本的浏览器都不支持document.createEvent()方法，因此我们需要另辟蹊径（据说IE有document.createEventObject()和event.fireEvent()方法，但是不支持自定义事件~~)。

##### IE浏览器有不少自给自足的东西，例如下面要说的这个"propertychange"事件，顾名思意，就是属性改变即触发的事件。例如文本框value值改变，或是元素id改变，或是绑定的事件改变等等。

##### 我们可以利用这个IE私有的东西实现自定义事件的触发，大家可以先花几分钟想想……

##### 大家现在有思路了没？其实说穿了很简单，当我们添加自定义事件的时候，顺便给元素添加一个自定义属性即可。例如，我们添加自定义名为"alert"的自定义事件，顺便我们可以对元素做点小手脚：

##### dom.evtAlert = "2012-04-01";

##### 再顺便把自定义事件fn塞到"propertychange"事件中：

```
dom.attachEvent("onpropertychange", function(e) {
    if (e.propertyName == "evtAlert") {
        fn.call(this);
    }
});
```

##### 这个，当我们需要触发自定义事件的时候，只要修改DOM上自定义的evtAlert属性的值即可：

```
dom.evtAlert = Math.random();	// 值变成随机数
```

##### 此时就会触发dom上绑定的onpropertychange事件，又因为修改的属性名正好是"evtAlert", 于是自定义的fn就会被执行。这就是IE浏览器下事件触发实现的完整机制，应该说讲得还是蛮细的。

##### 自定义事件的删除与触发事件不同，事件删除，各个浏览器都提供了对于的时间删除方法，如removeEventListener和detachEvent。不过呢，对于IE浏览器，还要多删除一个事件，就是为了实现触发功能额外增加的onpropertychange事件：
```
dom.detachEvent("onpropertychange", evt);
```