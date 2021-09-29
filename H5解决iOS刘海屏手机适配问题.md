# H5解决iOS刘海屏手机适配问题

## 操作步骤

1. 在meta里面添加viewport-fit解决

``` html

<meta name="viewport" content="width=device-width,user-scalable=no,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,viewport-fit=cover" />

```

其中

viewport-fit 有三个参数 

| 参数 | 含义 | 
| --- | --- |
| contain | 默认值(显示在安全区域以内) |
| cover | 占满全屏幕 |

2. 设置body的CSS

``` css

body{
  padding-top: env(safe-area-inset-top);
  padding-left: env(safe-area-inset-left);
  padding-right: env(safe-area-inset-right);
  padding-bottom: env(safe-area-inset-bottom);
  padding-top: constant(safe-area-inset-top);
  padding-left: constant(safe-area-inset-left);
  padding-right: constant(safe-area-inset-right);
  padding-bottom: constant(safe-area-inset-bottom);
}

```

其中 iOS11.2以上使用constant, iOS11.2以上使用env