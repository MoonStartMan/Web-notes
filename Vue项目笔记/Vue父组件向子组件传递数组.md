# Vue父组件向子组件传递数组

子组件标签部分
``` Title.vue
<template>
    <div>
        <div class="top-box">
            <div class="list"
                v-for="(list,index) in lists"
                :key="index"
                :style="{width:list.width}"
            >{{list.text}}</div>
        </div>
    </div>
</template>
```
子组件传值JS部分
```Vue.js
props: {
	lists:Array
}
```

父组件标签部分
```
<Title :lists="this.items"/>
```

父组件Vue.js部分
```
items:[

]
```