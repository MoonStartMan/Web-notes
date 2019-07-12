# Vue element-ui中的change事件传参问题

## HTML部分代码
``` html
<el-select v-model="value" placeholder="请选择" class="select" @change="changeResult($event,index)">
    <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
    >
    </el-option>
</el-select>
PS:change事件一定要加上$event参数，这样会将"选中的当前元素"和"传递的其他值"一起传递过去。
```

## JS部分代码
``` JavaScript
methods:{
        changeResult(index) {
            this.index = index;
            console.log(index);
        }
    }
```