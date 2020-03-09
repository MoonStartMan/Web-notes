# Vue-router路由守卫

``` JavaScript
router.beforeEach((to, from, next) => {
	console.log(to);	//	进入的页面(下一个页面)
	console.log(from); //  离开之前的页面(上一个页面)
	console.log(next);	//  
	next() // 没有传参数 直接进入to的页面
	//	next()传参数 会一直进行死循环
})
```

## 项目代码

### 路由守卫代码
``` JavaScript
router.beforeEach((to, from, next) => {
  let islogin = localStorage.getItem("token");
  islogin = Boolean(islogin);

  if(to.path == "/login"){
    if(islogin){
      next("/home");
    }else{
      next();
    }
  }else{
    if(to.meta.requireAuth && islogin) {
      next();
    }else{
      next("/login");
    }
  }
})
```

### 路由代码

``` JavaScript
import Vue from "vue";
import VueRouter from "vue-router";

Vue.use(VueRouter);

const routes = [
  {
    path: '/',
    redirect: '/login'
  },
  {
    path: "/login",
    name: "login",
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ "../views/Login.vue"),
  },
  {
    path: "/home",
    name: "Home",
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ "../views/Home.vue"),
    redirect: '/makecard',
    leaf: false,
    children: [
      // 卡片制作
      {
        path: '/makecard',
        name: 'makecard',
        component: () => import("../views/home/MakeCard.vue"),
        meta: {
          requireAuth: true
        }
      },
      // 用户列表
      {
        path: '/user',
        name: 'user',
        component: () => import("../views/home/User.vue"),
        meta: {
          requireAuth: true
        }
      },
      // 卡片详情
      {
        path: '/cardmess',
        name: 'cardmess',
        component: () => import("../views/home/CardMess.vue"),
        meta: {
          requireAuth: true
        }
      },
      // 留言管理
      {
        path: '/language',
        name: 'language',
        component: () => import("../views/home/Language.vue"),
        meta: {
          requireAuth: true
        }
      },
    ]
  }
];

const router = new VueRouter({
  mode: "history",
  base: process.env.BASE_URL,
  routes
});
```

1. 直接进入index的时候，参数to被改成了"index"，触发路由指向，就会跑beforeEach
2. 再一次 next 指向login，这时再次发生路由指向，再跑beforeEach，参数的to被改变成了"/login"
3. 白名单判断存在，则直接执行next(),因为没有参数,所以不会再次beforeEach。