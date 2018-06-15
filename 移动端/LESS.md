## LESS

### 传统CSS的缺点

CSS作为标记语言，语法相对简单，对使用者的要求较低 ，但同时也带来一些问题：

- CSS没有逻辑性，不方便维护及扩展，不利于复用 
- 对非前端工程师来说，很难写出组织良好且易于维护的CSS代码

### 简介

[LESS中文官网 ](https://less.bootcss.com/)

Less是一门CSS预处理语言，在CSS语言的基础上做了扩充，增加了诸如变量、混合（mixin）、函数等功能，让 CSS更易维护。

CSS与LESS的关系就像JavaScript与jQuery的关系。

- 提高CSS编写效率，减少大量重复代码的编写，让CSS更具有维护性、扩展性。
- 代码结构清晰，便于修改。 
- 让我们用类似JS的语法编写CSS代码。
- 完全兼容CSS代码，可以方便地应用到老项目中 。

### LESS编译器安装

**`由于各个编译器都有支持less的插件, 且简单易用, 所以可以忽略以下步骤`**

由于浏览器只认识CSS代码，所以需要将编写好的less文件转换为css文件后再拿到浏览器中运行。less官方提供了编译器，安装步骤如下：

- 由于less编译器依赖node环境,所以需要先安装node环境
  - 安装程序出现2502、2503错误解决方法
    - 以管理员身份运行cmd
    - msiexec /package 带文件名称的文件路径
  - 检测node是否安装成功
    - 打开命令行工具 win + r => cmd => 回车
    - node -v 查看安装node版本
    - npm  –v 查看npm版本
      - npm是node环境提供的下载工具 可以用它来下载less编译器
- 在线安装less
  - cmd中运行 npm install less -g
  - 检测less是否安装成功 lessc -v
- 离线安装
  - C:\Users\Administrator\AppData\Roaming\npm
  - 将Npm.Zip解压进去
- 在cmd中编译less文件
  - lessc less.less less.css
  - lessc 要编译的less文件 编译后的css文件
- [sublime text配置](http://www.jianshu.com/p/1ebf12edc967)
  - 安装sublime插件 less Less2Css
  - 安装依赖工具 在cmd中运行 npm install less-plugin-clean-css -g
- [Webstorm配置](http://www.jianshu.com/p/e99dc56d44c3)

### LESS语法学习

#### 注释

> 在代码中加入注释，对代码进行解释说明的方式。

| 多行注释              | 单行注释            |
| ----------------- | --------------- |
| /* 会被编译到CSS文件中 */ | // 不会被编译到CSS文件中 |

#### 变量(variable)

> LESS允许开发者自定义变量，使得样式修改起来更加方便，比如网页换肤功能(主体颜色)。

+ 将变量作为属性值使用

```less
@mainColor: #E93223;
body {
  color: @mainColor;
}
```

+ 将变量作为选择器使用

```less
// 值不能为字符串
@header: header;
.@{header} {
    color: @mainColor;
}
```

+ 将变量作为路径使用

```less
// 值必须为字符串
@imgUrl: '../images/';
.bgi {
  	// url 不要有空格
    background: url('@{imgUrl}1.jpg');
}
```

#### 混合(mixin)

> 混合就是一种将一系列属性从一个规格集引入到另一种规格集的方式, 主要用于定义公共样式; (类似于js中的函数, css中的类样式混合体)

1. 混合的基本使用, 公共样式被编译到CSS中

```less
// 公共样式
.border {
    border: 1px solid #e0e0e0;
}
h1 {
    font-size: 40px;
    .border;
}
h2 {
    font-size: 30px;
    .border;
}
// 编译后
.border {
  border: 1px solid #e0e0e0;
}
h1 {
  font-size: 40px;
  border: 1px solid #e0e0e0;
}
h2 {
  font-size: 30px;
  border: 1px solid #e0e0e0;
}
```

1. 禁止公共样式被编译到CSS中

```less
// 公共样式
.border() {
    border: 1px solid #e0e0e0;
}
h1 {
    font-size: 40px;
    .border;
}
h2 {
    font-size: 30px;
    .border;
}
// 编译后
h1 {
  font-size: 40px;
  border: 1px solid #e0e0e0;
}
h2 {
  font-size: 30px;
  border: 1px solid #e0e0e0;
}
```

1. 为公共样式传递参数

```less
.border(@size) {
    border: @size solid #e0e0e0;
}
h1 {
    font-size: 40px;
    .border(10px);
}
h2 {
    font-size: 30px;
    .border(20px);
}
// 编译之后
h1 {
  font-size: 40px;
  border: 10px solid #e0e0e0;
}
h2 {
  font-size: 30px;
  border: 20px solid #e0e0e0;
}
```

1. 为公共样式传递多个参数，参数之间用分号隔开

```less
.border(@size; @style; @color) {
    border: @size @style @color;
}
h1 {
    font-size: 40px;
    .border(10px; solid; skyblue);
}
h2 {
    font-size: 30px;
    .border(20px; solid; pink);
}
// 编译之后
h1 {
  font-size: 40px;
  border: 10px solid skyblue;
}
h2 {
  font-size: 30px;
  border: 20px solid pink;
}
```

1. 为公共样式提高优先级

```less
.border(@size; @style; @color) {
    border: @size @style @color;
    position: relative;
}
h1 {
    font-size: 40px;
    .border(10px;solid;skyblue) !important;
}
h2 {
    font-size: 30px;
    .border(20px; solid; pink);
}
// 编译后
h1 {
  font-size: 40px;
  border: 10px solid skyblue !important;
  position: relative !important;
}
h2 {
  font-size: 30px;
  border: 20px solid pink;
  position: relative;
}
```

#### 嵌套

> HTML结构具有嵌套性，而对应的CSS却是用空格表示父子级嵌套关系，看起来一点也不清晰。
> LESS中可以使用嵌套为CSS添加如同HTML一样的嵌套关系。

```less
#wjs_banner {
  .carousel-inner {
    > div.item {
      a.img_box {
        background: url("../images/slide_01_2000x410.jpg") no-repeat center center;
        height: 410px;
        /*调用redBorder mixin*/
        display: block;
        .redBorder();
        // &为直接父级选择器
        &:hover {
          /*调用@mainColor 变量*/
          color: @mainColor;
        }
      }
      a.img_mobile {
        width: 100%;
        display: block;
        img {
          width: 100%;
          display: block;
        }
      }
    }
  }
}
```

#### 导入

> 代码组织方式上的优化，可以将不同功能的代码放置在不同的文件中，起到归类的作用，方便维护。
> 比如可以将所有的变量放入一个文件中，将文件导入到当前文件中，就可以使用这些变量了。

```less
@import "base";
.f_left{
  float: @right;
}
```

**注意：如果导入的文件是 `.less` 扩展名，则可以将扩展名省略**

#### 内置函数

> Less 内置了多种函数用于转换颜色、处理字符串、算术运算等。

应用场景：

- 网站通常会有一个主色若干辅色，辅色的取值通常是在主色的基础上增加或减少亮度、透明度、饱和度。
- 通过判断当前值是否是某种类型，以达到输出不同样式的目的。

```less
ceil(@number); // 向上取整
floor(@number); // 向下取整
percentage(@number); // 将数字转换为百分比，例如 0.5 -> 50%
round(number, [places: 0]); // 四舍五入取整
abs(number); // * 数字的绝对值
pi(); // * 返回PI
red(@color); // 从颜色值中提取 'red' 值（红色）
green(@color); // 从颜色值中提取 'green' 值（绿色）
blue(@color); // 从颜色值中提取 'blue' 值（蓝色）
alpha(@color); // 从颜色值中提取 'alpha' 值（透明度）
saturate(@color, 10%); // 饱和度增加 10%
desaturate(@color, 10%); // 饱和度降低 10%
lighten(@color, 10%); // 亮度增加 10%
darken(@color, 10%); // 亮度降低 10%
fadein(@color, 10%); // 透明度增加 10%
fadeout(@color, 10%); // 透明度降低 10%
fade(@color, 50%); // 设定透明度为 50%
greyscale(@color); // 完全移除饱和度，输出灰色
iscolor(@colorOrAnything); // 判断一个值是否是颜色
isnumber(@numberOrAnything); // 判断一个值是否是数字（可含单位）
isstring(@stringOrAnything); // 判断一个值是否是字符串
isurl(@urlOrAnything); // 判断一个值是否是url
ispixel(@pixelOrAnything); // 判断一个值是否是以px为单位的数值
ispercentage(@percentageOrAnything); // 判断一个值是否是百分数
```

[完整函数手册](https://less.bootcss.com/functions/)

#### 条件判断

> 可以根据判断条件输出不同的样式。

```less
// 如果颜色中的亮度值大于等于50% 设置背景颜色为黑色
.mixin(@a) when( lightness(@a) >= 50%){
    background:#000;
}
// 如果颜色中的亮度值小于等于50% 设置背景颜色为白色
.mixin(@a) when(lightness(@a) <= 50%){
    background:#FFF;
}

.classA{
    // #ddd => rgb(221,221,221) 亮度高 输出背景黑色
    .mixin(#ddd);
}

.classB{
    // #555 => rgb(85,85,85) 亮度低 输出背景白色
    .mixin(#555)
}
```

#### 计算

```less
@back: #333;
.test {
  border: 1px solid @back*2;
  background: lighten(#000, 10%);
  color: darken(#000, 10%);
}
```

### 在页面中使用LESS

- 在html文档中引入编译之后的CSS文件
- 在页面中引入未编译好的CSS文件, 原less文件
  - **注意: 此方式只能用在开发阶段, 不能用于生产阶段**

```html
<!-- 引入未编译的less文件 -->
<link rel="stylesheet/less" type="text/css" href="styles.less" />
<!-- 引入插件less.js用于编译less文件 -->
<script src="less.js" type="text/javascript"></script>
```