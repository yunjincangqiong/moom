# swiper

## 简介

开源、免费、强大的移动端触摸滑动插件, 一款非常强大的轮播图插件

官网 http://www.swiper.com.cn

## 使用

```html
1.首先加载插件，需要用到的文件有swiper.min.js和swiper.min.css文件。

<!DOCTYPE html>
<html>
<head>
    ...
    <link rel="stylesheet" href="path/to/swiper.min.css">
</head>
<body>
    ...
    <script src="path/to/swiper.min.js"></script>
  	<!-- 如果你的页面加载了jQuery.js或者zepto.js，你可以选择使用更轻便的swiper.jquery.min.js -->
    <script src="path/to/jquery.js"></script>
    <script src="path/to/swiper.jquery.min.js"></script>
</body>
</html>

2.HTML样例布局。
!!!!!!!!!!核心为应用类名与标签无关!!!!!!!!!!
<div class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">Slide 1</div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
    </div>
    <!-- 如果需要分页器(点切换框) -->
    <div class="swiper-pagination"></div>
    
    <!-- 如果需要导航按钮(点击切换上下页) -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
    
    <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
</div>
导航等组件可以放在container之外

3.你可能想要给Swiper定义一个大小，当然不要也行。

.swiper-container {
    width: 600px;
    height: 300px;
}  

4.初始化Swiper：最好是挨着</body>标签
​~~~常用参数
direction : 轮播图的滑动方向，水平(horizontal默认值)或垂直(vertical)。
autoplay : 是否自动切换  ，默认不会自动切换false。
   autoplay: true; 等于以下设置
  /* autoplay: {
      delay: 3000,
      stopOnLastSlide: false,
      disableOnInteraction: true,
     } */
loop : 是否无缝滚动, 默认没有无缝滚动.
speed : 滑动速度，两张图片切换过度时间(默认为300ms 单位为ms)，也是触摸滑动时释放至贴合的时间.
autoplayDisableOnInteraction : 用户操作swiper之后，是否禁止autoplay。默认为true：停止。如果设置为false，用户操作swiper之后自动切换不会停止，每次都会重新启动autoplay。
keyboardControl : 是否开启键盘控制Swiper切换。设置为true时(默认值为false)，能使用键盘方向键控制轮播图滑动。
mousewheelControl : 是否开启鼠标控制Swiper切换。设置为true时(默认值为false)，能使用鼠标滚轮控制轮播图滑动。
paginationClickable : 此参数设置为true时(默认值为false)，点击分页器的指示点分页器会控制轮播图切换。
以下属性均会添加默认样式
nextButton : 点击显示下一张图片, 值为容器DOM元素'.swiper-button-next'.
prevButton : 点击显示上一张图片, 值为容器DOM元素'.swiper-button-prev'.
scrollbar : 在下方显示滚动条(注意实现无缝轮播时导航条显示不准确,因为前后各冬天添加了一张图片) 值为容器DOM元素'.swiper-scrollbar',
<script>        
    var mySwiper = new Swiper ('.swiper-container', {
        direction: 'vertical',
        loop: true,
        
        // 如果需要分页器
        pagination: '.swiper-pagination',
        
        // 如果需要前进后退按钮
        nextButton: '.swiper-button-next',
        prevButton: '.swiper-button-prev',
        
        // 如果需要滚动条
        scrollbar: '.swiper-scrollbar',
  })        
  </script>
</body>
如果不能写在HTML内容的后面，则需要在页面加载完成后再初始化。

<script type="text/javascript">
window.onload = function() {
  ...
}
</script>

或者这样（有query和Zepto类库）
<script type="text/javascript">
$(document).ready(function () {
 ...
})
</script>
5.完成。更多设置及参数参见网上文档API
http://www.swiper.com.cn/api/index.html
```

