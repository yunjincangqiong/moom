# mousewheel

## 简介

依赖于jQuery, 使原生 mousewheel(鼠标滚轮事件) 兼容个各个浏览器的插件

兼容性

+ 在谷歌浏览器和火狐浏览器所用的事件名称都不一样
+ 判断滚动方向的方式也不一样

注意: 

+ onscroll 不是滚轮事件, 是浏览器滚动条滚动事件, 但是也可以用滚轮控制(浏览器默认自带的能力)

## 使用

引入插件

```html
<script type="text/javascript" src="js/jquery.js"></script>
<script type="text/javascript" src="js/jquery.mousewheel.min.js"></script>
```

之后正常使用原生 mousewheel 事件即可

```html
<script>
  // 鼠标滚轮在滚动的时候 是戈登戈登的 戈登一次 事件处理函数触发一次
  $(document).on('mousewheel', function (e, delta) {
    // delta: 事件处理函数的第二个参数, 用来区分滚轮滚动的方向
    // 向上滚动 delta 为 1; 向下滚动 delte 为 -1
    // 更多参数 自行百度
  });
</script>
```

​             