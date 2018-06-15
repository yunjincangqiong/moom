# less(不建议使用)

用于将less文件转换为css文件

**注意: 此方式只能用在开发阶段, 不能用于生产阶段因为不近多引入一个js文件, 还增加了编译时间**

但是由于现在编译器都自带less转css插件并且非常好用, 所以该插件使用的频率非常低

```html
<!-- 引入未编译的less文件 -->
<link rel="stylesheet/less" href="styles.less" />
<!-- 引入插件less.js用于编译less文件 -->
<script src="less.js"></script>
```