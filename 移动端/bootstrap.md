## BootStrap

- 简洁、直观、强悍的前端响应式开发框架，让web开发更迅速、简单。
  - 将网站中一些常见组件的HTML和CSS以及JS提前定义好，使用者只需要复制粘贴，然后再根据需求修改即可，目的是减少开发难度，提高开发效率。
- [英文官网](http://getbootstrap.com)
- [中文官网](http://www.bootcss.com/)

### 移动设备优先

在 Bootstrap 3 中，我们重写了整个框架，使其一开始就是对移动设备友好的。这次不是简单的增加一些可选的针对移动设备的样式，而是直接融合进了框架的内核中。也就是说，**Bootstrap 是移动设备优先的**。针对移动设备的样式融合进了框架的每个角落，而不是增加一个额外的文件。

### 为什么要使用Bootstrap框架

- 使用人数众多，足够稳定，不断更新迭代
- 代码简洁、直观、规范
- 让开发更简单,提高了开发的效率
- 扩展性较强,可以自定义默认样式

### Bootstrap版本

- 2.x.x 停止维护
- 3.x.x 目前使用最多
  - 稳定，但是放弃了IE6-IE7。对IE8支持但是界面效果不好。偏向用于开发响应式布局、移动设备优先的Web项目。
- 4.x.x 测试阶段

### Bootstrap使用

#### 说明

**aria-开头的属性和role的属性均为兼容屏幕阅读器的属性**

#### 基本模板

以下引入文件均使用cdn网上文件, 需要联网;  无网络连接可下载到本地再引入

```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
      <script src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>

    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.min.js"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
  </body>
</html>
```

#### 布局容器

通常用于制作页面版心。

```html
<!-- 在不同的屏幕尺寸下布局容器的尺寸也是不同的 始终居中于屏幕 -->
<div class="container"></div>
<!-- 流式布局容器 容器宽度始终100% -->
<div class="container-fluid"></div>
```

#### 全局样式

设置全局CSS样式，对基本的HTML标签样式进行增强。包含排版、表格、表单、按钮、图片等等。[详见文档](https://v3.bootcss.com/css/)

#### 组件样式

包含网站用常见的组件样式，比如`导航条` , `媒体对象` , `字体图标`, 下拉菜单、警告框、弹出框(模态框)等等。[详见文档](https://v3.bootcss.com/components/) 

#### JavaScript 插件

Bootstrap依赖jQuery，提供了一些jQuery插件，比如`标签页`, `工具提示`, `模态框`轮播图插件(Carousel)，滚动监听插件，弹出框插件等等。[详见文档](https://v3.bootcss.com/javascript/)

##### JavaScript 轮播图

```html
<!-- 
  以下容器就是整个轮播图组件的整体，
  注意该盒子必须加上 class="carousel slide" data-ride="carousel" 表示当前是一个轮播图
  bootstrap.js会自动为当前元素添加图片轮播的特效
-->
<div id="轮播图的ID" class="carousel slide" data-ride="carousel">
  <!-- ol标签是图片轮播的控制点 -->
  <ol class="carousel-indicators">
    <!-- 
      每一个li就是一个单独的控制点
        data-target属性就是指定当前控制点控制的是哪一个轮播图，其目的是如果界面上有多个轮播图，便于区分到底控制哪一个
        data-slide-to属性是指当前的li元素绑定的是第几个轮播项
      注意，默认必须给其中某个li加上active(通常是第一个)，展示的时候就是焦点项目
    -->
    <li data-target="#轮播图的ID" data-slide-to="0" class="active"></li>
    <li data-target="#轮播图的ID" data-slide-to="1"></li>
    <!-- ...更多的 -->
  </ol>
  <!-- 
    .carousel-inner是所有轮播项的容器盒子，
    注意role="listbox"代表当前div是一个列表盒子，作用就是给当前div添加一个语义
  -->
  <div class="carousel-inner" role="listbox">
    <!-- 每一个.item就是单个轮播项目，注意默认要给第一个轮播项目加上active，表示为焦点 -->
    <div class="item active">
      <!-- 轮播项目中展示的图片, 也可使用北京图片 -->
      <img src="example.jpg" alt="示例图片">
      <div class="carousel-caption">
        <!-- 标题或说明性文字，如果不需要，直接删除当前div.carousel-caption -->
      </div>
    </div>
    <div class="item">
      <!-- ... -->
    </div>
    <!-- ... -->
  </div>
  <!-- 图片轮播上左右两个控制按钮，分别点击可以滚动到上一张和下一张 -->
  <!-- 此处需要注意的是 该a链接的href属性必须指向需要控制的轮播图ID -->
  <!-- 另外a链接中的data-slide="prev"代表点击该链接会滚到上一张，如果设置为next的话则相反 -->
  <a class="left carousel-control" href="#轮播图的ID" role="button" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
    <span class="sr-only">上一张</span>
  </a>
  <a class="right carousel-control" href="#轮播图的ID" role="button" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">下一张</span>
  </a>
</div>
```

##### 标签页

**导航和内容两部分可以单独使用, 注意id值不重复且相对应即可**

```html	
<div>

  <!-- 标签导航 -->
  <ul class="nav nav-tabs" role="tablist">
    <!-- li标签的class="active"为当前选中的标签 -->
    <!-- a标签的href属性为切换内容的id -->
    <li role="presentation" class="active"><a href="#home" aria-controls="home" role="tab" data-toggle="tab">Home</a></li>
    <li role="presentation"><a href="#profile" aria-controls="profile" role="tab" data-toggle="tab">Profile</a></li>
    <li role="presentation"><a href="#messages" aria-controls="messages" role="tab" data-toggle="tab">Messages</a></li>
    <li role="presentation"><a href="#settings" aria-controls="settings" role="tab" data-toggle="tab">Settings</a></li>
  </ul>

  <!-- 标签内容 -->
  <div class="tab-content">
    <!-- div标签的class="active"为当前显示的标签内容 -->
    <!-- id值与标签导航中a标签的href属性相对应 -->
    <div role="tabpanel" class="tab-pane active" id="home">...</div>
    <div role="tabpanel" class="tab-pane" id="profile">...</div>
    <div role="tabpanel" class="tab-pane" id="messages">...</div>
    <div role="tabpanel" class="tab-pane" id="settings">...</div>
  </div>

</div>
```

##### 工具提示

```html
<!-- data-placement提示文字的位置, title提示的文字 -->
<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="top" title="Tooltip on top">Tooltip on top</button>
<!-- js初始化 -->
<style>
  $(function () {
    $('[data-toggle="tooltip"]').tooltip()
  })
</style>
```

#### 栅格系统

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。下面就介绍一下 Bootstrap 栅格系统的工作原理：

- “行（row）”必须包含在 `.container` （固定宽度）或 `.container-fluid` （100% 宽度）中，以便为其赋予合适的排列（aligment）和内补（padding）。
- 通过“行（row）”在水平方向创建一组“列（column）”。
- 你的内容应当放置于“列（column）”内，并且，只有“列（column）”可以作为行（row）”的直接子元素。
- 如果一“行（row）”中包含了的“列（column）”大于 12，多余的“列（column）”所在的元素将被作为一个整体另起一行排列。
- 栅格类适用于与屏幕宽度大于或等于分界点大小的设备

```html
<!-- 响应式容器 -->
<div class="container">
  <!-- 通过类名row创建行 -->
  <div class="row">
    <!-- 通过col-md-数值 类名创建列 -->
    <div class="col-md-6">内容1</div>
    <div class="col-md-6">内容2</div>
  </div>
</div>
```

- Bootstrap将一行默认分为12列(可以更改默认值)，可以通过类名中的数值来定义当前列占总列数的份数。

- 使用格式:  col-\*-*  

- 第一个\*为屏幕大小, 第二个\*为份数(0-12)

  - lg 当屏幕宽度 ≥1200px 时生效
  - md 当屏幕宽度 ≥992px 时生效
  - sm 当屏幕宽度 ≥768px 时生效
  - xs 当屏幕宽度 ≥320px  时生效

- 列偏移

  说明: 第一个\*为屏幕大小, 第二个\*为偏移格数(0-12)

  - 使用 .col-\*-offset-\* 类可以将列向右侧偏移，设置列与列之间的间距。
    - 使用的margin来调整间距, 后面的元素会随着一起改变位置
  - .col-\*-pull-\* 将列向左侧移动
  - .col-\*-push-\* 将列向右侧移动
    - 以上两个使用的定位进行移动所以可能会有覆盖的效果

- 列嵌套

  - 列中可以再次嵌套栅格系统，称为列嵌套，以支撑复杂的网页布局。

    ```html
    <div class="row">
        <div class="col-md-6">
            <div class="row">
                <div class="col-md-6"></div>
                <div class="col-md-6"></div>
            </div>
        </div>
        <div class="col-md-6"></div>
    </div>
    ```

#### 工具类

4大颜色名: 

.success            浅绿背景

.error              红色背景

.warning            黄色背景

.info               浅蓝背景

可配合text-\*, btn-* 使用

| 类名称            | 解释                        |
| -------------- | ------------------------- |
| text-left      | 文本左对齐                     |
| text-center    | 文本居中对齐                    |
| text-right     | 文本右对齐                     |
| center-block   | 让块级元素居中                   |
| pull-left      | 左浮动                       |
| pull-right     | 右浮动                       |
| clearfix       | 清除浮动                      |
| show           | 显示元素                      |
| hidden         | 隐藏元素                      |
| hidden-xs      | 只在超小屏幕中隐藏                 |
| hidden-sm      | 只在小屏幕中隐藏                  |
| hidden-md      | 只在中等屏幕中隐藏                 |
| hidden-lg      | 只在大屏幕中隐藏                  |
| btn            | 将a, button, input 显示为按钮样式 |
| btn-default    | 默认按钮样式                    |
| btn-link       | 连接按钮样式                    |
| table          | 具有表格的基本样式                 |
| table-striped  | 内容斑马线背景(隔行变色)             |
| table-bordered | 加表格边框                     |
| table-hover    | 内容鼠标进入高亮                  |
