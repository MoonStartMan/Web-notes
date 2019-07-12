# CSS3 cubic-bezier

## 三次赛贝尔简介：

cubic-bezier 又称三次贝塞尔，用四个点（p0,p1,p2,p3）描绘一条曲线。
在css3中，p0默认为（0，0），p3默认为（1，1）。所以，我们只需关注p1，p2。
在css3动画中，用来表示速度曲线。

## 三次赛贝尔曲线作用：

### 在CSS3 中的动画效果中，设置速度运动曲线。
### 在CSS3 中使用：

``` css
animation-timing-function: cubic-bezier(x1,y1,x2,y2);
```

## 计算公式

### 公式：B(t) = P0(1 - t)3 + 3P1t(1 - t)2+3P2t2(1 - t) + P3t3,  t ∈ [0, 1];(括号后的3和2分别为立方和平方)