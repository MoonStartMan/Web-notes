# Vue双重循环点击事件

## template代码

``` html
<div class="check-box">
                <div class="check-box-item" v-for="(box, index) in checkLists" :key="index">
                    <div class="left">
                        {{box.type}}
                    </div>
                    <div class="right">
                        <div class="right-itemList">
                            <div class="right-item" 
                                v-for="(item, i) in box.lists"
                                :key="i"
                                @click="addClass(index,i)"
                                :class="{active:isActive[index][0]==index&&isActive[index][1]==i}"
                            >
                                {{item.name}}</div>
                        </div>
                    </div>
                </div>
            </div>
```

Ps: 第二个v-for需要在第一个v-for的item里面，列如(item,index) in box.lists

## JavaScript代码

``` JavaScript
name: "colleges",
    data() {
        return {
            value: '',  //  搜索值
            isActive:[  //  点击的值
                [0,0],
                [1,0],
                [2,0],
                [3,0],
            ], 
            checkLists: [
                {
                    id: 0,
                    type: "学校地区:",
                    lists: [
                        {
                            id: 0,
                            name: "不限",
                        },
                        {
                            id: 1,
                            name: "安徽"
                        },
                        {
                            id: 2,
                            name: "北京"
                        },
                        {
                            id: 3,
                            name: "重庆"
                        },
                        {
                            id: 4,
                            name: "福建"
                        },
                        {
                            id: 5,
                            name: "甘肃"
                        },
                        {
                            id: 6,
                            name: "贵州"
                        },
                        {
                            id: 7,
                            name: "广东"
                        },
                        {
                            id: 8,
                            name: "湖北"
                        },
                        {
                            id: 9,
                            name: "海南"
                        },
                        {
                            id: 10,
                            name: "黑龙江"
                        },
                        {
                            id: 11,
                            name: "湖南"
                        },
                        {
                            id: 12,
                            name: "河南"
                        },
                        {
                            id: 13,
                            name: "河北"
                        },
                        {
                            id: 14,
                            name: "吉林"
                        },
                        {
                            id: 15,
                            name: "江西"
                        },
                        {
                            id: 16,
                            name: "江苏"
                        },
                        {
                            id: 17,
                            name: "辽宁"
                        },
                        {
                            id: 18,
                            name: "宁夏"
                        },
                        {
                            id: 19,
                            name: "内蒙古"
                        },
                        {
                            id: 20,
                            name: "青海"
                        },
                        {
                            id: 21,
                            name: "山西"
                        },
                        {
                            id: 22,
                            name: "山东"
                        },
                        {
                            id: 23,
                            name: "陕西"
                        },
                        {
                            id: 24,
                            name: "四川"
                        },
                        {
                            id: 25,
                            name: "上海"
                        },
                        {
                            id: 26,
                            name: "天津"
                        },
                        {
                            id: 27,
                            name: "西藏"
                        },
                        {
                            id: 28,
                            name: "新疆"
                        },
                        {
                            id: 29,
                            name: "云南"
                        },
                        {
                            id: 30,
                            name: "浙江"
                        },
                    ]
                },
                {
                    id: 1,
                    type: "学校类型:",
                    lists: [
                        {
                            id: 0,
                            name: "不限"
                        },
                        {
                            id: 1,
                            name: "综合"
                        },
                        {
                            id: 2,
                            name: "语言"
                        },
                        {
                            id: 3,
                            name: "工科"
                        },
                        {
                            id: 4,
                            name: "医药"
                        },
                        {
                            id: 5,
                            name: "体育"
                        },
                        {
                            id: 6,
                            name: "财经"
                        },
                        {
                            id: 7,
                            name: "艺术"
                        },
                        {
                            id: 8,
                            name: "名族"
                        },
                        {
                            id: 9,
                            name: "师范"
                        },
                        {
                            id: 10,
                            name: "林业"
                        },
                        {
                            id: 11,
                            name: "农业"
                        },
                        {
                            id: 12,
                            name: "政法"
                        },
                    ]
                },
                {
                    id: 2,
                    type: "学校级别:",
                    lists: [
                        {
                            id: 0,
                            name: "不限"
                        },
                        {
                            id: 1,
                            name: "本科"
                        },
                        {
                            id: 2,
                            name: "专科"
                        },
                    ]
                },
                {
                    id: 3,
                    type: "著名学校:",
                    lists: [
                        {
                            id: 0,
                            name: "不限"
                        },
                        {
                            id: 1,
                            name: "985"
                        },
                        {
                            id: 2,
                            name: "211"
                        },
                        {
                            id: 3,
                            name: "双一流"
                        },
                    ]
                },
            ]
        }
    },
    methods: {
        addClass(index,i) {
            this.isActive[index][0] = index; 
            this.isActive[index][1] = i;
            this.$forceUpdate();    //  强制重新渲染
        }
    }
```

Ps: vue无法识别深层的渲染，需要用this.$forcreUpdate()进行强制重新渲染。