# twbsPagination

## 简介

依赖于 jQuery, 一款分页插件

## 使用

定义一个容器存放分页导航

```html
<div id="twbsPagination"></div>
```

引入插件

```html
<script src="assets/vendors/jquery/jquery.min.js"></script>
<script src="assets/vendors/twbs-pagination/jquery.twbsPagination.min.js"></script>
```

初始化插件

```html
<script>
// 容器调用 twbsPagination 函数
$('#pagination').twbsPagination({
  // 总页数
  totalPages: info.pages,
  // 显示的分页按钮个数
  visiblePages: 5,
  // 更改上一页按钮文本
  prev: '上一页',
  // 更改下一页按钮文本
  next: '下一页',
  // 点击所有任何分页按钮触发事件
  // 第二个参数为点击的页数(数字类型)
  onPageClick: function (event, page) {
    // 逻辑代码
  })
</script>
```

