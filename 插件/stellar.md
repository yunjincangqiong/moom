# stellar

## 简介

[stellar.js](https://github.com/markdalgleish/stellar.js/) 是一个基于 jQuery 的插件, 能很容易地给网站添加视差滚动效果. 尽管已经停止了维护，但它非常稳定，与最新版本的jQuery兼容，很多开发者也在使用它。 这个插件在[jQuery插件库](http://plugins.jquery.com/)里很流行。

http://markdalgleish.com/projects/stellar.js/   官网

## 原理

改变元素的背景的 background-position 属性与页面的移动速度成比例

改变元素的 top, left, bottom, right 属性与页面的移动速度成比例(此元素要定位)

## 参数

| 名称                                      | 说明                                       |
| --------------------------------------- | ---------------------------------------- |
| horizontalScrolling 和 verticalScrolling | 该配置项用来设置视差效果的方向。horizontalScrolling设置水平方向，verticalScro设置垂直方向， 为布尔值，默认为true |
| responsive                              | 该配置项用来制定load或者resize时间触发时是否刷新页面，其值为布尔值，默认为false |
| hideDistantElements                     | 该配置项用来设置移出视线的元素是否隐藏，其值为布尔值，若不想隐藏则设置为false` |
| data-stellar-ratio="2"                  | 定义了此元素针对页面滚动的速度比率，比如，0.5为页面滚动的50%，2为页面滚动的200%，所以数值越大，你可以看到页面元素滚动速度越快。 |
| data-stellar-background-ratio           | 该配置项用在单个元素中，其值为一个正数，用来改变被设置元素的影响速度。 例如 值为0.3时，则表示背景的滚动速度为正常滚动速度的0.3倍。如果值为小数时最好在样式表中设置 |

## 使用

### html基本结构

```html
<style>
  .dv {
    background: url('./images/header.png') no-repeat;
  }
</style>
<!-- 设置背景的移动速度比 -->
<div class="dv" data-stellar-background-ratio=".5"></div>
<!-- 设置元素的移动速度比 -->
<div data-stellar-ratio="-2">
  <img src="./images/1.png">
</div>
```

### 插件引入

```html
<script src="./libs/jquery.min.js"></script>
<script src="./libs/jquery.stellar.js"></script>
```

### 初始化

```html
<script>
  $(function () {
    $.stellar({
      // 页面尺寸发生改变重新渲染页面
      responsive: true,
      // 横向无视差滚动效果(默认为true)
      horizontalScrolling: false
    })
  });
</script>
```

