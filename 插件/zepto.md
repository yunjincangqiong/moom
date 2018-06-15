# zepto

## 简介

此插件主要用于移动端 (移动端的jquery), 可理解为阉割版的 jQuery , 语法用法相同
不同点为 : 此插件去除了兼容的部分只支持高版本浏览器
特点: 此插件为 模块化 插件
调用时使用那个模块导入那个模块(详情见网上文档)

**由于jQuery3.0版本之后体积也很小, 也使用css3的新属性, 所以移动端使用zepto的人也开始变少**

## 使用

### 常用模块

```html
<!-- 核心模块(常用选择器等) -->
<script src="lib/zepto/zepto.min.js"></script>
<!-- 扩展选择器 -->
<script src="lib/zepto/selector.js"></script>
<!-- 动画 -->
<script src="lib/zepto/fx.js"></script>
<!-- 手势 -->
<script src="lib/zepto/touch.js"></script>
```

```html
1. 调用文件
2. 入口函数 
  $(function(){
      代码;
  });
```

