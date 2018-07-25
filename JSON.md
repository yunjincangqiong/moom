## 简介

JSON ( JavaScript Object Notation, JS 对象标记) 是一种轻量级的数据交换格式。它基于 ECMAScript ( 欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

json基本的两种格式

- '["html", "css", "javascript"]'
- '{"name": "gt", "age": "15"}'
- 注意:
  - 键必须用 " 双引号包裹
  - 最后一个值, 不能以 , 逗号结尾
  - 其中不能有注释
  - 没有 `undefined` 这个值

**大多数语言都内置了相应的 json 数据处理 api**

### javascript-api

+ JSON.parse(json)
  + 用于解码 json 数据
+ JSON.stringify(json)
  + 用于编码 json 数据

#### js兼容老ie

```html
使用 json2.js 来兼容老ie, ie8以下版本没有定义 JSON 的问题, 在 head 中引入以下代码即可
<!-- 用来解决 JSON 在 IE 低版本下未定义的问题 -->
<!-- 以下为 IE 能识别的注释, 其他浏览器或者高版本ie会忽略此代码 -->
<!-- ie hack -->
<!--[if lte IE 7]>
<script src="json2.js"></script>
<![endif]-->
```

### php-api

- json_decode(json数据[, true])    
  - 将json数据转化成数组和对象的格式, 第二个参数就是将数据转化成纯数组(将对象转化为关联数组)的形式
  - php中解码json数据时, 注意json中如果有对象数据, 建议使用第二个参数 true, 数据好处理
- json_encode(json数据)
  - 将数据转化成json数据

