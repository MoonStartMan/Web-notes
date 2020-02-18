# Vue Watch初始化执行一次与监听router参数方法

## Vue watch方法初始化执行一次

### 例子 watch监听账号和密码 显示高亮

``` vue.js
<template>
	<div>
		<input type="text" v-model="number" placeholder="请输入账号" maxlength="16">
		<input type="password" v-model="password" placeholder="请输入密码" maxlength="16">
	</div>
</template>

<script>
data() {
	return {
		number: 'admin1',
		password: '123456'
	}
},
computed: {
	numChange() {
		const {number, password} = this;
		return {number, password}
	}
},
//  高亮
watch: {
	numChange: {
	//   handler执行函数
		handler: function(val) {
  if((val.number.length>=6&&val.number.length<=16)&&(val.password.length>=6&&val.password.length<=16)) {
          this.isActive = true;
        } else {
          this.isActive = false;
        }
      },
      immediate: true  // 默认初始化执行一次
	}
}
</script>
```

## 监听router参数变化的方法

``` vue.js
watch: {
	$route() {
		console.log(this.$route.query.参数)
	}
}
```