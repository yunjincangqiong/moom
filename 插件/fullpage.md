# fullpage

## 简介

是一个基于 jQuery 的插件，它能够帮你很方便、很轻松的制作出全屏网站。

http://www.dowebok.com/demo/2014/77/    演示地址

## 原理

包含 mousewheel 鼠标滚轮事件

## 主要功能

支持鼠标滚动

支持前进后退和键盘控制

多个回调函数

支持手机、平板触摸事件

支持 CSS3 动画

支持窗口缩放

窗口缩放时自动调整

可设置滚动宽度、背景颜色、滚动速度、循环选项、回调、文本对齐方式等等

## 引用文件

**!!!!!注意jQuery版本不要太高, 否则会报错!!!!!!**

```html
<!-- 插件css -->
<link rel="stylesheet" href="js/fullpage/jquery.fullpage.min.css">
<!-- 页面css -->
<link rel="stylesheet" href="css/index.css">

<!-- jQuery -->
<script src="js/jquery/jquery.js"></script>
<!-- 插件js -->
<script src="js/fullpage/jquery.fullpage.min.js"></script>
```

## HTML 结构

```html
<div id="fullpage">
  	<!-- section 为竖向整屏 -->
    <div class="section">第一屏</div>
    <div class="section">第二屏</div>
    <div class="section">
      	<!-- slide 为横向整屏 -->
        <div class="slide">第三屏的第一屏</div>
        <div class="slide">第三屏的第二屏</div>
        <div class="slide">第三屏的第三屏</div>
        <div class="slide">第三屏的第四屏</div>
    </div>
    <div class="section">第四屏</div>
</div>
```

## fullpage初始化

```javascript
$(function(){
  	// fullpage 函数有可选参数为一个对象
    $('#fullpage').fullpage();
});
```

## fullpage常用参数

```text
verticalCentered 内容是否垂直居中
sectionsColor 竖屏的颜色 值为数组 ["red","green"]
slidesColor 横屏的颜色 值为数组
scrollingSpeed 切屏过度时间(ms)
navigation 项目导航(导航点图)
```

## fullpage详细参数

### 属性

| 选项                                | 类型   | 默认值         | 说明                                   |
| --------------------------------- | ---- | ----------- | ------------------------------------ |
| sectionsColor                     | 数组   | 无           | 竖屏幕背景颜色                              |
| slidesNavPosition                 | 字符串  | bottom      | 定义滑块的横向导航栏的位置                        |
| verticalCentered                  | 字符串  | true        | 内容是否垂直居中                             |
| resize                            | 布尔值  | false       | 字体是否随着窗口缩放而缩放                        |
| slidesColor                       | 数组   | 无           | 横屏幕背景颜色                              |
| anchors                           | 数组   | 无           | 定义锚链接                                |
| scrollingSpeed                    | 整数   | 700         | 滚动速度，单位为毫秒                           |
| easing                            | 字符串  | easeInQuart | 滚动动画方式                               |
| menu                              | 布尔值  | false       | 绑定菜单，设定的相关属性与 anchors 的值对应后，菜单可以控制滚动 |
| navigation                        | 布尔值  | false       | 是否显示项目导航                             |
| navigationPosition                | 字符串  | right       | 项目导航的位置，可选 left 或 right              |
| navigationColor                   | 字符串  | #000        | 项目导航的颜色                              |
| navigationTooltips                | 数组   | 空           | 项目导航的 tip                            |
| slidesNavigation                  | 布尔值  | false       | 是否显示左右滑块的项目导航                        |
| slidesNavPosition                 | 字符串  | bottom      | 左右滑块的项目导航的位置，可选 top 或 bottom         |
| controlArrowColor                 | 字符串  | #fff        | 左右滑块的箭头的背景颜色                         |
| loopBottom                        | 布尔值  | false       | 滚动到最底部后是否滚回顶部                        |
| loopTop                           | 布尔值  | false       | 滚动到最顶部后是否滚底部                         |
| loopHorizontal                    | 布尔值  | true        | 左右滑块是否循环滑动                           |
| autoScrolling                     | 布尔值  | true        | 是否使用插件的滚动方式，如果选择 false，则会出现浏览器自带的滚动条 |
| scrollOverflow                    | 布尔值  | false       | 内容超过满屏后是否显示滚动条                       |
| css3                              | 布尔值  | false       | 是否使用 CSS3 transforms 滚动              |
| paddingTop                        | 字符串  | 0           | 与顶部的距离                               |
| paddingBottom                     | 字符串  | 0           | 与底部距离                                |
| fixedElements                     | 字符串  | 无           |                                      |
| normalScrollElements              |      | 无           |                                      |
| keyboardScrolling                 | 布尔值  | true        | 是否使用键盘方向键导航                          |
| touchSensitivity                  | 整数   | 5           |                                      |
| continuousVertical                | 布尔值  | false       | 是否循环滚动，与 loopTop 及 loopBottom 不兼容    |
| animateAnchor                     | 布尔值  | true        |                                      |
| normalScrollElementTouchThreshold | 整数   | 5           |                                      |

### 回调函数

| 名称             | 说明                                       |
| -------------- | ---------------------------------------- |
| afterLoad      | 滚动到某一屏后的回调函数，接收 anchorLink 和 index 两个参数，anchorLink 是锚链接的名称，index 是序号，从1开始计算 |
| onLeave        | 滚动前的回调函数，接收 index、nextIndex 和 direction 3个参数：index 是离开的“页面”的序号，从1开始计算；nextIndex 是滚动到的“页面”的序号，从1开始计算；direction 判断往上滚动还是往下滚动，值是 up 或 down。 |
| afterRender    | 页面结构生成后的回调函数，或者说页面初始化完成后的回调函数            |
| afterSlideLoad | 滚动到某一水平滑块后的回调函数，与 afterLoad 类似，接收 anchorLink、index、slideIndex、direction 4个参数 |
| onSlideLeave   | 某一水平滑块滚动前的回调函数，与 onLeave 类似，接收 anchorLink、index、slideIndex、direction 4个参数 |

### fullPage.js 方法

**调用时使用(JQ函数挂载机制)  $.fn.fullpage.函数名();**

| 名称                     | 说明                      |
| ---------------------- | ----------------------- |
| moveSectionUp()        | 向上滚动                    |
| moveSectionDown()      | 向下滚动                    |
| moveTo(section, slide) | 滚动到                     |
| moveSlideRight()       | slide 向右滚动              |
| moveSlideLeft()        | slide 向左滚动              |
| setAutoScrolling()     | 设置页面滚动方式，设置为 true 时自动滚动 |
| setAllowScrolling()    | 添加或删除鼠标滚轮/触控板控制         |
| setKeyboardScrolling() | 添加或删除键盘方向键控制            |
| setScrollingSpeed()    | 定义以毫秒为单位的滚动速度           |

## 样例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>购物网站宣传页面</title>
  	<!-- 引入css -->
    <link rel="stylesheet" href="css/jquery.fullpage.min.css">
    <link rel="stylesheet" href="css/index.css">
</head>
<body>
<!--更多精彩-->
<div class="more"><img src="images/00-more.png" alt=""></div>
<!--全屏滚动-->
<div class="container">
    <section class="section"></section>
    <section class="section"></section>
    <section class="section"></section>
    <section class="section"></section>
    <section class="section"></section>
    <section class="section"></section>
    <section class="section"></section>
    <section class="section"></section>
</div>
<!-- 引入js -->
<script src="js/jquery.min.js"></script>
<script src="js/jquery.fullpage.min.js"></script>
<script>
    $(function() {
      	// 父元素调用 fullpage 函数
        $('.container').fullpage({
          	// 内容不垂直居中
            verticalCentered: false,
          	// 竖屏背景颜色
            sectionsColor: ["#fadd67", "#84a2d4", "#ef674d", "#ffeedd", "#d04759", "#84d9ed", "#8ac060"],
          	// 显示项目导航
            navigation: true,
          	// 项目导航显示在右侧
          	navigationPosition: 'right',
          	// 屏幕切换过度事件(ms)
            scrollingSpeed:1000,
            //页面初始化完成后的回调函数
            afterRender: function () {
                $('.more').on('click', function () {
                    /*切换下一页*/
                    /*jquery的插件封装机制  基于  $.fn.fullpage */
                    $.fn.fullpage.moveSectionDown();
                });
            },
          	// 离开某一页触发的回调函数
            onLeave: function (index, nextIndex, direction) {},
        });
    })
</script>
```

