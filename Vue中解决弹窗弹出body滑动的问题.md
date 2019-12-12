# Vue中解决弹窗弹出body滑动的问题

## 安装插件 

```
npm install tua-body-scroll-lock --save-dev 
```

## 在组件中引用

``` JavaScript
import { lock, unlock } from 'tua-body-scroll-lock'
lock()	//	锁住
unlock()	//	解锁
```