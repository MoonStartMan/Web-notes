# Vue中嵌套swiper导致图片大小不相等问题解决办法

这个是由于显示不完整造成的BUG，需要在Option选项中监听盒子的变化，触发刷新

``` javascript

swiperOptions: {
	observer: true,
	observeParents: true
}

```

如果高度出现问题，则还需要添加一行代码,如下:

``` javascript

swiperOptions: {
	autoHeight: true
}

```