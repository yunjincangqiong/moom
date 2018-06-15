# iscroll

## 简介

移动端 使元素内部的子元素可以滑动

## 使用

html格式

```html
<!-- 父元素 -->
<div id="parent">
  <!-- 需要一个盒子包裹, 插件将所有的属性应用在子盒子中 -->
  <div calss="child">
    内容
  </div>
</div>
```

```html
1. 插件引入
<script src="./libs/iscroll.js"></script>
2. 初始化
<script>
    // 注意横纵移动的条件为宽或高大于父元素
    // 直接父元素需要设置 overflow:hidden;
  	// 第一个参数为可滚动元素的直接DOM父元素, #id也可
    // 第二个参数为可选参数, 只需要简单滚动时, 可不写该参数
	var myScroll = new IScroll('#parent' ,{
        scrollX: true,  // 横向移动
        scrollY: true, // 纵向移动(默认可以纵向移动)
        tap: true      // 允许在滚动的范围内使用 tap 事件(iscroll插件封装)
    });

  	// 将该元素滚动置顶
  	myScroll.scrollToElement(内容里面的元素)
</script>
```

## 样例

**注意引用插件**

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    html,
    body {
      height: 100%;
    }

    .nav {
      position: relative;
      height: 100%;
      width: 90px;
      overflow: hidden;
      background: orange;
    }

    .nav .scroll {
      position: absolute;
      left: 0;
      top: 0;
    }

    .nav .scroll a {
      display: block;
      width: 90px;
      height: 50px;
      line-height: 50px;
      border-right: 1px solid #ccc;
      border-bottom: 1px solid #ccc;
      text-align: center;
    }

    .nav .scroll a.active {
      background-color: #fff;
      border-right: 1px solid transparent;
    }
  </style>
</head>

<body>
  <div class="nav" id="nav">
    <div class="scroll">
      <a class="nav-text active" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
      <a class="nav-text" href="javascript:;">热门推荐</a>
    </div>
  </div>

  <script src="./js/iscroll/iscroll.js"></script>
  <script>
    // 只需要简单的滚动 new IScroll('#nav');
    var myScroll = new IScroll('#nav', {
      tap: true
    });
    document.querySelector('.scroll').addEventListener('tap', scrollFn);
    var as = document.querySelectorAll('.scroll a');

    function scrollFn(e) {
      if (e.target.nodeName.toUpperCase() === 'A') {
        // 将当前点击的 a 元素置顶
        myScroll.scrollToElement(e.target);
        as.forEach(function (v, i) {
          v.className = '';
        });
        e.target.className = 'active';
      }
    }
  </script>
</body>

</html>
```



​	