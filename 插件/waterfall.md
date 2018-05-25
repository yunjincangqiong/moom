# waterfall

## 简介

图片瀑布流插件, 用于大量图片展示

## 使用

### html结构

```html
<div class="items">
  <div class="item">
    <img src="url" width="" height="" />
    <p>文字信息</p>
  </div>
  <div class="item">
    <img src="url" width="" height="" />
    <p>文字信息</p>
  </div>
  <!-- ...(重复n个) -->
</div>
```

### 插件引入

```html
<!-- jQuery 库 -->
<script src="./libs/jquery-1.12.4.min.js"></script>
<!-- 瀑布流插件 -->
<script src="./libs/jquery.waterfall.js"></script>
```

### 初始化

```html
<script>
  $(function () {
    // 获取外面的父元素
    $('items').waterfall({
      // 列距离(px)
      gap: 15
    })
  });
</script> 
```

## 主要应用 ajax 分页

每次动态向后台获取一定数量的图片数据并动态添加到页面中, 每获取一次就初始化一次

