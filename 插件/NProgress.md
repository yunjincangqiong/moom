# NProgress

## 简介

将文件加载完成度显示成进度条的插件, 一般配合 ajax 使用

进度条走到接近最后, 会一直保持那个长度(与结尾位置有一点距离)不变, 但是加载圈一直转

## 使用

引入文件

```
<link rel="stylesheet" href="./assets/vendors/nprogress/nprogress.css">
<script src="../assets/vendors/nprogress/nprogress.js"></script>
```

在开始请求文件时, 添加下面的语句

+ NProgress.start()

在请求文件完成时, 添加下面的语句

+ NProgress.done()

设置进度条的百分比

+ NProgress.set(0.6)

增加一点进度条进度

+ NProgress.inc()