## 原生JS动态修改播放音乐
+ 修改source的src属性不起作用: 需要在audio.play()之前加一个audio.load();
+ 背景音乐不能马上播放，需要用户操作或者加一个延时操作。