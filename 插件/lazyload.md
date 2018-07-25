# lazyload

## 简介

基于 jQuery 的图片懒加载插件

## 原理

判断下面的图片与当前显示页面位置的距离, 达到一定数值后动态设置 img 的 src 属性

## 使用

### 说明

```
* 结构中 img 标签的 data-original 自定义属性是必须的，就是用这个属性存储着图片的路径
* 图片的宽度和高度属性也是必须的, 占据相应的空间, 防止布局混乱
* 调用懒加载的方法的对象必须是 img 标签
```

### html基本结构

```html
<div class="wrapper">
  <img class="lazy" data-original="images/01.jpg" alt="" width="1280" height="800" >
  <img class="lazy" data-original="images/02.jpg" alt="" width="1280" height="800" >
  <img class="lazy" data-original="images/03.jpg" alt="" width="1280" height="800" >
  <img class="lazy" data-original="images/04.jpg" alt="" width="1280" height="800" >
</div>
```

### 引入插件

```html
<script src="js/jquery-1.12.2.min.js"></script>
<script src="./libs/jquery.lazyload.min.js"></script>
```

### 初始化插件

```javascript
$(function () {
  // 所有 懒加载图片 调用 lazyload 方法
  $('.lazy').lazyload();
});
```

