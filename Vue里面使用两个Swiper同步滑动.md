# Vue里面使用两个Swiper同步办法

## HTML部分
``` html
<swiper :options="swiperOption" ref="mySwiper" class="bg-swiper">
                    <!-- slides -->
                    <swiper-slide v-for="item of swiperList" :key="item.id" class="bg-swiper-slide">
                        <img :src="item.imgUrl" alt="" class="bg-swiper-img"/>
                    </swiper-slide>
                </swiper>
                <div class="sm-swiper-cover">
                    <swiper :options="smSwiperOption" ref="mySwiper2" class="sm-swiper">
                        <swiper-slide class="sm-swiper-slide" v-for="item of smSwiperList" :key="item.id">
                            <img :src="item.imgUrl" alt="" class="sm-swiper-img">
                            <div class="swiper-text">{{item.text}}</div>
                        </swiper-slide>
                    </swiper>
                    <div class="navigation-pre">
                        <img src="../../assets/detialsImg/left-arrow.png" alt="">
                    </div>
                    <div class="navigation-next">
                        <img src="../../assets/detialsImg/right-arrow.png" alt="">
                    </div>
                </div>
```

## JS部分

``` JavaScript
swiperOption: {
                notNextTick: true,
                direction: "horizontal",
                loop: true,
                on: {
                    slideChange: () => {
                        let swiper = this.$refs.mySwiper.swiper;
                        let index = swiper.realIndex;
                        this.changeSwiper(index);
                    },
                },
            },
            
// 校园风光菜单swiper配置,
            smSwiperOption: {
                notNextTick: true,
                loop: true,
                direction: "horizontal",
                slidesPerView : 4,
                spaceBetween: 10,
                slideToClickedSlide: true,
                navigation: {
                    nextEl: '.navigation-next',
                    prevEl: '.navigation-pre',
                },
                on: {
                    slideChange: () => {
                        let swiper = this.$refs.mySwiper2.swiper;
                        let index = swiper.realIndex;
                        this.changeSwiper(index);
                    },
                    click: () => {
                        let swiper = this.$refs.mySwiper2.swiper;
                        let index = swiper.realIndex;
                        this.changeSwiper(index);
                    }
                },
            }
```

Ps: 

``` JavaScript
on:function() {
	this.
}	//	this 无法指向vuedata里面的数据
//	需要使用es6箭头函数
on: () => {
	let swiper = this.$refs.mySwiper2.swiper;
	let index = swiper.realIndex;
	this.changeSwiper(index);
}

为了获取索引值正确值，必须要在菜单栏的swiper里面设置
``` JavaScript
slideToClickedSlide: true,
//	否则点击的时候 realIndex的值都是当前页面的值，列如总共有五个swiper-slide，一页展示4个，前四个的realIndex永远是0.
```
```