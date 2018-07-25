# css

## position

### 绝对定位

未指定 left/top/right/bottom 的 absolute元素，其在所处层级中的定位点就是正常文档流中该元素的定位点

如果同时设置left和right会水平拉伸，同时设置top和bottom会垂直拉伸

隐藏一个元素(不扰乱布局, 获取不到焦点): absolute + left: -3000px; absolute + visibility: hidden

## 权重问题

+ 正常情况下或者权重相同时, 后面的样式权重高

### 文件引入方面

+ 用户自定义样式 10000
+ !important  1000
+ 行内样式 100
+ 内部样式 / 外链样式 / 导入样式(@import) 10
+ 浏览器默认样式 1

### css写法方面

+ id 1000
+ 类 / 伪类 / 属性 100
+ 元素 / 伪元素 10
+ `*` 1

## 属性

### 伪元素

+ css2之前使用 : 访问; css3之后使用 :: (建议使用)访问, 向后兼容css2写法

#### ::before

```
特殊属性 content: value; 一般为字符串,常用于空值;注意即使为空值也要写
before显示为元素内部的第一个子元素,并显示content中的内容,鼠标不可选中,默认为行内元素
一般用于产生特殊图形
attr()函数 可将元素中的自定义属性中的值取出放在content中
例: 
html:
	<div data-text="演示文本"></div>
css:
	div::before {
      content: attr(data-text);//此处相当于content: "演示文本";
	}
```

#### ::after

```
同上 显示为元素内部的最后一个子元素 
一般用于清除浮动 
例: 
css:
	.clearFlo::after {
      content: '';
      clear: both;
      display: block;//清除浮动必须为块级元素
    }
```





