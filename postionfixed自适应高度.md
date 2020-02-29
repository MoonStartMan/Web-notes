# postion:fixed自适应高度

``` CSS
.mask {
/*需要宽度*/
  width: 70%;
  background-color: white;
  position: fixed;
  left: 50%;
  top: 50%;
  /* 支持现代浏览器 */
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
```

当使用：top: 50%;left: 50%;， 是以左上角为原点，故不处于中心位置 translate(-50%,-50%) 作用是，往上（x轴）,左（y轴）移动自身长宽的 50%，以使其居于中心位置。