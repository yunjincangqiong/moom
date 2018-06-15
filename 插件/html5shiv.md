# html5shiv

## 简介

解决 IE9 以下不支持 HTML5 语义化标签问题

## 原理

使用 document.createElement(html5语义化标签) 和 css 属性 display: block; 使ie低版本兼容html5语义化标签

## 使用

```html
<!-- 只有 IE9 以下版本浏览器不支持, 其他浏览器去加载就冗余降低加载效率, 使用ie条件注释, 解决此问题 -->
<!-- head 头部引入插件 -->
<!--[if lt IE 9]>
  <script src="./libs/html5shiv.min.js"></script>
<![endif]-->
```

## ie条件注释

**快捷键 cc:ie + tab**

```html
<!--[if lt IE 9]> 
	这里面的内容只有相应版本的ie会识别, 其余浏览器把其当成普通注释处理 
<![endif]-->  
lt 小于  gt  大于  lte 小于等于  gte 大于等于
```

