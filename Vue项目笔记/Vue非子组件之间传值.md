# Vue非子组件之间传值
需求：组件A点击之后B组件接收到值，A组件根据B组件的值再进行隐藏或者显示

## 创建公共仓库来存值bus.js
``` vue.js
import Vue from 'vue'
export default new Vue()
```

## 组件A先发送
``` vue.js
<script>
 // 引入公共的bug，来做为中间传达的工具
 import Bus from './bus.js'
 export default {
  data () {
   return {
    brandFold: true
   }
  },
  methods: {
  changeState(){
  	this.brandFold = !this.brandFold;
  	Bus.$emit('val',this.brandFold)
  	}
  },
  components:{ 
  	Bus
  }
 }
</script>
```

## 组件B接收
```
data: function() {
    return {
        state: ""
    }
},
mounted: function() {	//接收
        var that = this;
        Bus.$on('val',(data)=>{
            that.state = data;
        })
    },
    methods:{
        changState: function() {
            this.state = !this.state
        }
    },
```

## B组件再向A组件发送
```
 methods:{
        changState: function() {
            this.state = !this.state
            Bus.$emit('val2',this.state)
        }
    },
```

## A组件再接收B组件进行改变
```
mounted:function(){
        var that = this
        Bus.$on('val2',(data) => {
            if(data) {//判断是否已经隐藏
                this.brandFold = !data
            }
        })
    },
```