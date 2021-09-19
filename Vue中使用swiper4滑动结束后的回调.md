# Vue中使用swiper4滑动结束后的回调

## 第一步安装低版本Swiper

``` shell

npm install swiper@4.x vue-awesome-swiper --save-dev

```

## 完成Swiper配置

### 在temple中书写Swiper

``` html

<swiper :options="swiperOption" ref="mySwiper" class="swiper">
  <!-- slides -->
  <swiper-slide v-for="item of swiperList" :key="item.id">
    <img 
      :src="item.img" 
      alt="" 
      class="img"
      @click="gotoClick(item.id)"
    >
  </swiper-slide>
  <!-- swiper-pagination -->
  <div class="swiper-pagination" slot="pagination"></div>
</swiper>

```

### 在script中配置swiper

#### 首先在data里面完成swiper的一些基本配置

``` javascript

swiperOption: {
  notNextTick: true,
  autoplay: {
    delay: 3000,
    stopOnLastSlide: false,
    disableOnInteraction: false,
  },
  direction: "horizontal",
  loop: true,
  speed: 3000,
  pagination: {
    el: ".swiper-pagination",
    type: "bullets",
    clickable: true,
    bulletClass: "my-bullet",
    bulletActiveClass: "my-bullet-active",
    bulletElement: "li",
  }
},

```

#### 在computed配置swiper方便后面在slider滑动结束后设置方法

``` javascript

computed: {
swiper() {
  return this.$refs.mySwiper.$swiper
  }
}

```

#### 设置滑动结束后的方法

``` javascript

mounted() {
  let vm = this;
  this.swiper.on('slideChangeTransitionEnd', function() {
    vm.currentIndex = this.realIndex
  })
}

```