# art-template

## 简介

腾讯旗下的一款开源的模板引擎: 主要用于前端渲染数据

[中文文档](https://aui.github.io/art-template/zh-cn/index.html)

## 特性

1. 拥有接近 JavaScript 渲染极限的的性能
2. 调试友好：语法、运行时错误日志精确到模板所在行；支持在模板文件上打断点（Webpack Loader）
3. 支持 Express、Koa、Webpack
4. 支持模板继承与子模板
5. 浏览器版本仅 6KB 大小

## 原生语法

类似于 html标签格式 加原生 js语法, 可以写在模板定义语句中的任何位置

+ 语句用 <% js语句 %> 包含
+ 输出语句用 <%= js语句 %> 包含

###样例

```html
<!-- html代码 -->
<div class="carousel-inner"></div>
<!-- 引入模板引擎插件 -->
<!-- 引入插件之后全局中就多了一个 template 函数 -->
<script src="./libs/template-web.js"></script>
<!-- 模板定义 -->
<script type="text/template" id="imagesHtml">
  <% for(var i = 0; i < list.length ; i++) {%>
    <div class="item <%= i==0? 'active':'' %>">
      <% if (!isM){ %>
      <a href="#" style="background-image: url('<%= list[i].pcUrl %>')"></a>
      <% } else { %>
      <a href="#"><img src="<%= list[i].mUrl %>" alt="图片"></a>
      <% } %>
    </div>
  <% } %>
</script>
<!-- js代码部分 -->
<script>
  // 使用格式: template(模板id,{自定义数据}); 返回 html 代码
  // 返回 html 字符串
  var imagesHtml = template("imagesHtml", {
    list: data, // data一般为向后台请求的 json 数据
    isM: isM // 可以自定义键值对
  });
  // 将 html 字符串添加到父元素中
  $(".carousel-inner").html(imagesHtml);
</script>
```

## 简洁语法

```html
<script type="text/template" id="test">
// 遍历数组  v: 为值 i: 为索引
{{each data as v i}}
// 如果数据中存在特殊符号 < > / 等, 前面加一个 # 号不让其转义正常显示数组
<img src="{{#v.img}}" src="图片">
{{/each}}
</script>
```



