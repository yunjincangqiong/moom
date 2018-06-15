# Normalize.css

## 简介

使所有元素在所有浏览器中表现保持一致

与 reset 的异同点

共同点：都是重置样式库，增强浏览器的表现一致性

不同点：
举个例子：ul
reset.css   list-style:none ---因为需求
normalize.css 不会重置ul样式 ---本身已经在每个浏览器表现一致的元素

一句话：都是增强浏览器的表现一致性但是normalize不会重置已经一致的元素

创造 normalize.css 的目的：

- 保护有用的浏览器默认样式而不是完全去掉它们
- 一般化的样式：为大部分HTML元素提供
- 修复浏览器自身的bug并保证各浏览器的一致性
- 优化CSS可用性：用一些小技巧

## 使用

```html
<!-- 在 head 中直接引入即可 -->
<head>
	<link rel="sheetstyle"  href="./libs/normalize.css" />
</head>
```

