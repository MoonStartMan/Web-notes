# Vue子组件向父组件传递值

## 子组件
``` html
<div class="left-menu" @click="show()">
    <div class="menu-text">全部彩种</div>
    <div class="iconfont icon-xiajiantou"
    :class="[state ? 'transf': '']"
    ></div>
</div>
```

``` JavaScript
methods: {
    show() {
        this.state = !this.state
        this.$emit("sendState",this.state)
    }
},
```

## 父组件
``` html
<Header @sendState="getState"/>
```

``` js
import Header from '../../components/mobile/Header'
 methods: {
     getState(data) {
     	this.state = data;
     }
 }
```