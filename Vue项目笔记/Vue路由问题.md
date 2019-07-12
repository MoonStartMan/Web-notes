# Vue-router综合杂症
## Vue获取当前路由

```	vue.js
watch: {
    $route(to, from){
        console.log(this.$route.path);
    }
}
```

## vue-router去掉下划线
``` css
a {
    text-decoraction: none;
}
.router-link-active{
    text-decoration: none;
}
```

## vue-router 刷新当前页面
### 原因：移动端开发，菜单点击切换路由，菜单挡住内容部分。
``` vue
<div class="container">
	<div class="menu-img" @click="changeState()"></div>
</div>
 <div class="menu-lists"
 v-for="(menu, index) in menus"
 :key="index"
 @click="changeState()"
 >
 <router-link 
 :to="{path:menu.url}">
 <span class="iconfont" 
 :class="setClass(index+1)"
 :style="{color: menu.style}"
 ></span>
 <span class="menu-list">{{menu.text}}</span>
 </router-link>
 </div>
```

``` vue.js
methods: {
    setClass(index) {
    	let obj = {face: true}
    obj[`icon-mb${index}`] = true
    	return obj
    },
    changeState(){
    	this.brandFold = !this.brandFold;
    }
}
```
点击来回切换state，控制隐藏实现刷新。

## vue-router去掉"#"
``` router.js
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

mode改为history模式

## Vue-router配置+默认跳转子路由+整合PC+Mobile
``` router.js
routes: [
    {
      path: "/",
      redirect: "/index"
    },
    {
      path: "/index",
      component: resolve => require(["@v/Index"], resolve),
      children: [
        {
          path: "/",
          component: resolve => require(["@v/pc/Index"], resolve)
        }
      ]
    },
    {
      path: "/mobile",
      name: "mobile",
      redirect: '/MobileHome',
      component: resolve => require(["@v/Mobile"], resolve),
      children: [
        {
          path: "/MobileHome",
          component: resolve => require(["@v/mobile/Home"], resolve)
        },
        {
          path: "/MobileWeijie",
          component: resolve => require(["@v/mobile/Weijie"], resolve)
        },
        {
          path: "/MobileYijie",
          component: resolve => require(["@v/mobile/Yijie"], resolve)
        },
        {
          path: "/MobileQuery",
          component: resolve => require(["@v/mobile/Query"], resolve)
        },
        {
          path: "/MobileResult",
          component: resolve => require(["@v/mobile/Result"], resolve)
        },
        {
          path: "/MobileRule",
          component: resolve => require(["@v/mobile/Rule"], resolve)
        }
      ]
    }
```
默认子路由关键字:redirect

## Vue根据不同的路由显示不同的Header
``` vue
<div class="content" v-if="showId == 0">
	不同内容
</div>
<div class="content" v-if="showId == 1">
	不同内容
</div>
<div class="content" v-if="showId == 2">
	不同内容
</div>
<div class="content" v-if="showId == 3">
	不同内容
</div>
```

``` vue.js
data: function() {
        return {
            showId: 0
        }
    },
    watch: {
        '$route'(to, from) {
            console.log(this.$route.path)
            if(this.$route.path == "/MobileHome") {
                this.showId = 0;
            }
            if(this.$route.path == "/MobileResult") {
                this.showId = 1;
            }
            if(this.$route.path == "/MobileWeijie") {
                this.showId = 2;
            }
            if(this.$route.path == "/MobileYijie") {
                this.showId = 3;
            }
        }
    },
```