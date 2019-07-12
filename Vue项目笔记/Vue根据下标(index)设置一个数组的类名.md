# Vue根据下标(index)设置一个数组的类名

## HTML部分代码
``` html
<div class="list-right">
    <div class="list-number"
        v-for="(number,index) in list.numbers"
        :key="index"
        :class="setClass(index)"
        >
        {{number.text}}
    </div>
</div>
```

## less部分代码
``` less
.list-number{
    width: 1.3rem;
    height: 1.3rem;
    display: flex;
    display: -webkit-flex;
    justify-content: center;
    align-items: center;
    font-size: .7rem;
    color: #ffffff;
    border-radius: .2rem;
}
.list-number.bg1{
	background-color: #FFFD3C;
}
.list-number.bg2{
    background-color: #008CFA;
}
.list-number.bg3{
	background-color: #4D4D4D;
}
.list-number.bg4{
	background-color: #FF7022;
}
.list-number.bg5{
	background-color: #77FFFD;
}
.list-number.bg6{
	background-color: #4224F8;
}
.list-number.bg7{
	background-color: #E3E3E3;
}
.list-number.bg8{
	background-color: #FF001A;
}
.list-number.bg9{
	background-color: #790007;
}
.list-number.bg10{
	background-color: #32C533;
}
```

## JS部分代码
``` JavaScript
methods: {
    setClass(index) {
    	return "bg"+ (index+1)
    }
}
```