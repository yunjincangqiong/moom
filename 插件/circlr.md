# circlr

## 简介

基于jQuery, 一个利用多张不同角度的图片, 完成360度横向旋转的展示效果的插件

## 使用

html样例模板

```html
<!-- 包裹图片的父盒子, 一定要有 id -->
<div class="container" id="circlr">
  <!-- 图片url存储在自定义属性 data-src 中 -->
  <img data-src="images/00.jpg">
  <img data-src="images/01.jpg">
  <img data-src="images/02.jpg">
  <img data-src="images/03.jpg">
  <img data-src="images/04.jpg">
  <img data-src="images/05.jpg">
  <img data-src="images/06.jpg">
  <img data-src="images/07.jpg">
  <img data-src="images/08.jpg">
  <img data-src="images/09.jpg">
  <img data-src="images/10.jpg">
  <img data-src="images/11.jpg">
  <img data-src="images/12.jpg">
  <img data-src="images/13.jpg">
  <img data-src="images/14.jpg">
  <img data-src="images/15.jpg">
  <!-- 存储加载动画的盒子, 一定要有 id -->
  <div class="loading" id="loader"></div>
</div>
```

插件导入

```html
<script type="text/javascript" src="js/jquery.js"></script>
<script type="text/javascript" src="js/circlr.min.js"></script>
```

插件初始化

```html
<script>
  circlr('circlr', { // circlr是图片父级ID
    scroll : true,   // 滚轮也可以转动图片
    loader : 'loader' // loading图标容器ID
  });
</script>
```

