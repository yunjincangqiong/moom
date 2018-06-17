## 简介

+ AJAX（Asynchronous JavaScript and XML）(异步 javascript 和 XML)，最早出现在 2005 年的 [Google Suggest](http://google-suggest.tumblr.com/)，是在浏览器端进行网络编程（发送请求、接收响应）的技术方案，它使我们可以通过 JavaScript 直接获取服务端最新的数据而不必重新加载页面。让 Web 更能接近桌面应用的用户体验。

## 原生ajax

### readyState(状态码)

由于 `readystatechange` 事件是在 `xhr` 对象状态变化时触发（不单是在得到响应时），也就意味着这个事件会被触发多次，所以我们有必要了解每一个状态值代表的含义：

| readyState | 状态描述             | 说明                                   |
| ---------- | ---------------- | ------------------------------------ |
| 0          | UNSENT           | 代理（XHR）被创建，但尚未调用 `open()` 方法。        |
| 1          | OPENED           | `open()` 方法已经被调用，建立了连接。              |
| 2          | HEADERS_RECEIVED | `send()` 方法已经被调用，并且已经可以获取状态行和响应头。    |
| 3          | LOADING          | 响应体下载中， `responseText` 属性可能已经包含部分数据。 |
| 4          | DONE             | 响应体下载完成，可以直接使用 `responseText`。       |

+ 总结: 状态码 4 最有用其他了解即可

###响应体

+ responseText
  + 后台返回的数据为字符串格式
+ responseXML
  + 后台返回的数据为 XML(可拓展标记语言) 格式, 已经过时, 被 json 替代

### XML

+ eXtensible Markup Language 可拓展标记语言
+ 主要用来传输和存储数据, 前端领域 json 数据格式使用比较多, XML 使用比较少
+ 了解: 微信聊天数据, 手机锁屏推送数据都是 XML 格式

```text
xml 和 html 对比:
1. xml 与 html 都属于标记语言，都由标签构成
2. xml 与 html 类似都有其固定的结构
   a) 文档声明
   b) 都要有一个根元素
3. xml 是用来存储数据的，html 是用来展示数据的
4. html 的标签都是预定义的，xml 标签可以自定义（甚至是中文）

语法:
1. 文档声明必须顶格写，前面不能有任何内容（空行也不行）
2. 必须且只有一个根元素
3. 标签可以自定义，但是不能以数字（特殊符号）开头
4. 标签必须闭合
5. 标签属性也可以自定义，属性值必须使用双引号（注：单引也不报错）
6. 注释与html一样
7. xml 具有自我描述性（标签名一般说明了数据类型）
```

XML 样例数据

```xml
<?xml version="1.0" encoding="UTF-8"?>
<users>
	<user>
		<name>刘德华</name>
		<age>58</age>
		<gender>男</gender>
	</user>
	<user>
		<name>王力宏</name>
		<age>40</age>
		<gender>男</gender>
	</user>
</users>
```

可以使用 DOM 解析 XML 数据

样例: 使用上面的 XML 文件演示解析

```javascript
$.ajax({
  // 请求一个 XML 文件
  url: './users.xml',
  type: 'get',
  success: function (data) {
    var doc = data;
    // 获取所有的 user 标签
    var users = doc.getElementsByTagName('user');
    // 遍历标签获取其中的数据,  获取之后渲染添加即可
    for(var i = 0; i < users.length; i++) {
      console.log(users[i].getElementsByTagName('name')[0].innerHTML);
      console.log(users[i].getElementsByTagName('age')[0].innerHTML);
      console.log(users[i].getElementsByTagName('gender')[0].innerHTML);
    }
  }
});
```

### 遵循 HTTP 

+ 本质上 XMLHttpRequest 就是 JavaScript 在 Web 平台中发送 HTTP 请求的手段，所以我们发送出去的请求任然是 HTTP 请求，同样符合 HTTP 约定的格式：

```javascript
// 设置请求报文的请求行
xhr.open('GET', './time.php')
// 设置请求头
xhr.setRequestHeader('Accept', 'text/plain')
// 设置请求体
xhr.send(null)

xhr.onreadystatechange = function () {
  if (this.readyState === 4) {
    // 获取响应状态码
    console.log(this.status)
    // 获取响应状态描述
    console.log(this.statusText)
    // 获取响应头信息
    console.log(this.getResponseHeader('Content-Type')) // 指定响应头
    console.log(this.getAllResponseHeader()) // 全部响应头
    // 获取响应体
    console.log(this.responseText) // 文本形式
    console.log(this.responseXML) // XML 形式，了解即可，不用了
  }
}
```

### get方式请求

```javascript
// 创建一个 ajax 实例
var xhr = new XMLHttpRequest();
// 调用 readystatechange 事件
xhr.onreadystatechange = function () {
  // 判断 readyState 状态, 和 status 状态码
  if (xhr.readyState === 4 && xhr.status === 200) {
    // 处理相应信息
    console.log(xhr.responseText);
  }
}
// 建立与服务器的连接, 向后台发送的数据拼接在 url 后面发送
// 键值对信息格式：key1=value1&key2=value2
xhr.open('get', url?键值对信息);
// get 方式, send 方法参数为 null 或者 不写
xhr.send(null);
```

### post方式请求

```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(xhr.responseText);
  }
}
xhr.open('post', url);
// post 请求必须设置此请求头
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
// post 向后台发送数据, 写在 send 里
// 键值对信息格式：key1=value1&key2=value2
xhr.send(键值对信息);
```

## 同步和异步

###同步

正常代码的执行都是同步执行, 代码从上到下从左到右依次执行, 遇见请求数据时, 会等待数据返回才会继续向下执行代码, 否则就一直等待.

open 的第三个参数为异步执行代码, 默认值为 true, 设置为 false 时为代码同步执行

```javascript
var xhr = new XMLHttpRequest();
// 设置 open 的第三个参数
// 将第3个参数设置为 false 才可以以 同步方式执行
xhr.open('get', 'async.php', false);
xhr.send();
// 同步方式，无需要事件监听
console.log(xhr.responseText);
console.log('代码要等到响应完成才执行');
```

### 异步

遇见请求数据时, 不会等待数据返回会继续向下执行代码.

凡事 大多数情况下 涉及到回调函数 的都可以认为是 异步方式 在执行代码。

## jQuery 中的 AJAX

### $.ajax

+ 一个基本的案例

```javascript
$.ajax({
  // 请求地址
  url: './get.php',
  // 情趣类型
  type: 'get',
  // 向后台发送的数据
  data: { 'id': 1 },
  // 数据成功返回, 处理数据
  success: function (data) {
    console.log(data)
  }
})
```

####常用选项参数介绍

属性:

- url：请求地址

- type：请求方法，默认为 `get`

- data：需要传送到服务端的数据, 为对象类型

- dataType：服务端响应数据类型

  - 预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断

    - 如果后端代码中设置了响应头, 例如 php 代码  header('Content-Type: application/json'), jQuery 会将返回的数据调用JSON.parse()处理, 直接返回解码好的 json 数据.

  - 注意: 一般情况下只有设置值为 jsonp 时才添加此属性

  - 服务端响应数据类型种类

    - ```
      "xml": 返回 XML 文档，可用 jQuery 处理。
      "html": 返回纯文本 HTML 信息；包含的 script 标签会在插入 dom 时执行。
      "script": 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了 "cache" 参数。注意：在远程请求时(不在同一个域下)，所有 POST 请求都将转为 GET 请求。（因为将使用 DOM 的 script标签来加载）
      "json": 返回 JSON 数据 。
      "jsonp": JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。
      "text": 返回纯文本字符串
      ```

- contentType：请求体内容类型，默认 `application/x-www-form-urlencoded`

- timeout：请求超时时间默认单位为秒( s )

方法:

- success：请求成功之后触发（响应状态码 200）
  - 有一个参数, 一般写为 data 是后台返回的数据
- beforeSend：请求发起之前触发, 一般常用于浏览器端检测用户数据, 
  - 特殊 return false 时, 不会发送 ajax 请求
- error：请求失败触发, 有两参数
  - 第一个参数: 为错误对象,
    - 常用属性   statusText: 错误信息;   status:  http 状态码
  - 第二个参数为 字符串 'error'
- complete：请求完成触发（不管成功与否）

### $.get()

```javascript
// 简化 get 请求
// $.get 专门发送 get 请求
// 相当于 $.ajax({type: 'get'})

// 可以是三个参数
// 1) 请求地址
// 2) 请求参数
// 3) 成功回调
// $.get('get.php');
// $.get('get.php', {name: 'xiaoming', age: 16});
$.get('get.php', {name: 'xiaoming', age: 16}, function (data) {
	console.log(data);
});
```

### $.post()

```javascript
// 简化 post 请求
// $.post 专门用于发起 post 请求
// 相当于 $.ajax({type: 'post'})

// 可以是 三个参数
// a) 请求地址
// b) 请求参数
// c) 回调函数
// $.post('post.php');
// $.post('post.php', {name: 'xiaohong', age: 18});
$.post('post.php', {name: 'xiaohong', age: 18}, function (data) {
  console.log(data);
});
```

##模拟$.ajax请求封装

```javascript
$ = {
  ajax: function (data) {
    // 获取相应的参数的值, 并设置其默认值
    var url = data.url || location.href;
    var type = data.type || 'GET';
    var data1 = data.data || {};
    var dataType = data.dataType || 'json';
    var success = data.success || function () {};
    var newData = '';
    for (var key in data1) {
      newData += key + '=' + data1[key] + '&';
    }
    // 去掉末尾的 & 字符, 获取通用传递参数   格式 $key1=$value1&$key2=$value2...
    newData = newData.slice(0, -1);
    // 同源访问
    if (dataType === 'json') {
      var xhr = new XMLHttpRequest();
      // 设置 send 函数的通用参数, 默认为get 请求的 null 值
      var sendData = null;
      if (type.toUpperCase() === 'GET') {
        xhr.open('GET', url + '?' + newData);
      }
      if (type.toUpperCase() === 'POST') {
        xhr.open('POST', url);
        // 设置请求头
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        // 设置为通用的传递参数
        sendData = newData;
      }
      xhr.send(sendData);
      xhr.addEventListener('readystatechange', function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          var resData = this.responseText;
          // 获取 Content-Type 相应头的值
          var resHeader = this.getResponseHeader('Content-Type');
          // 如果后台设置了 json 数据的响应头
          if (resHeader.indexOf('json') !== -1) {
            // 将其进行 json 数据解码
            resData = JSON.parse(this.responseText);
          }
          // 将数据传入回调函数
          success(resData);
        }
      });
      // 结束当前程序执行
      return;
    }

    // jsonp 跨域部分
    if (dataType.toLowerCase() === 'jsonp') {
      // 创建一个不重复的函数名
      var cbName = '_gt_' + Date.now();
      // 将函数名暴露给全局变量, 使其可以随处访问
      window[cbName] = function (data) { 
        // 将数据传递给回调函数
        success(data);
      };
      // 创建 script 标签
      var script = document.createElement('script');
      // 设置 src 属性, 拼接 url 
      script.src = url + '?callback=' + cbName + '&' + newData;
      // 将其添加到 body 标签中
      document.body.appendChild(script);
    }
  }
}
```

## 跨域

涉及多地址设置请移步至 [相关软件的安装.md](./相关软件的安装.md)

###浏览器同源策略

同源策略是浏览器的一种安全策略，两个不同源的网址请求数据时浏览器会阻止其发生并报错.

####同源

所谓同源是指域名(1,2级域名都相同)，协议，端口(默认为80端口)完全相同，只有同源的地址才可以相互通过 AJAX 的方式请求。

同源或者不同源说的是两个地址之间的关系，不同源地址之间请求我们称之为**跨域请求**

例如：http://www.example.com/detail.html 与以下地址对比

| 对比地址                                     | 是否同源 | 原因        |
| ---------------------------------------- | ---- | --------- |
| http://api.example.com/detail.html       | 不同源  | 2级域名不同    |
| https://www.example.com/detail.html      | 不同源  | 协议不同      |
| http://www.example.com:8080/detail.html  | 不同源  | 端口不同      |
| http://api.example.com:8080/detail.html  | 不同源  | 2级域名、端口不同 |
| https://api.example.com/detail.html      | 不同源  | 协议、2级域名不同 |
| https://www.example.com:8080/detail.html | 不同源  | 端口、协议不同   |
| http://www.example.com/other.html        | 同源   | 只是文件路径不同  |

### 解决方案

有时浏览器的同源策略会阻止我们想要的结果, 比如同一家公司的两个不同的网站请求数据也会被阻止.

以下为常用的解决方案

####jsonp(非官方的解决方案)

名词解释:  jsonp( json with padding ) 填充式json / 参数式json

#####原生jsonp

原理：

1. 通过 script 标签的 src 属性的跨域访问能力, 在 url 末尾传入一个参数
2. 服务端接收此参数, 并使用此参数返回一段 JavaScript 函数调用数据

完整的 jsonp 样例

```javascript
// javascript 代码
// 封装一个 jsonp 函数
function jsonp (url, fn) {
  // 拼接一个不重复的函数名
  var fnName = '_gt_' + Date.now();
  // 将函数暴露给全局变量, 使其可以随处调用
  window[fnName] = function (data) {
    // 将数据传递给回调函数
    fn(data);
  }
  // 动态创建 script 标签 将其添加到 body 元素中
  var script = document.createElement('script');
  // 设置其 src 属性, 将函数名以参数的形式传递给后端
  script.src = url + '?callback=' + fnName;
  // 将创建好的 script 元素添加到 body 元素中
  // script 标签会被解析执行, 向指定 url 发送请求
  document.body.appendChild(script);
}
// 调用封装好的 jsonp 函数
// 回台返回的js代码会被自动解析执行(script标签的能力)
jsonp('http://www.gt.com/test1.php', function (data) {
  // 处理后台返回的数据
  console.log(data);
});
```

```php
// php 代码
// 模拟数据
$arr = ['name'=>'gt', 'age'=>12];
// 接收传递过来的函数名
$fnName = $_GET['callback'];
// 返回函数名和作为其实参的数据
echo $fnName.'('. json_encode($arr) .');';
```

问题: 为什么只能用 get 请求

原因: 要使用script 标签的 src 跨域能力, src 请求只能为 get 请求

#####jQuery -- jsonp

```javascript
$.ajax({
  url: 请求地址,
  // 只能为 get 请求
  type: 'get',
  // 设置 dataType 属性
  dataType: 'jsonp',
  success: function (data) {
    console.log(data);
  }
})
```

#### CORS(官方解决方案)

名词解释: Cross Origin Resource Share，跨域资源共享

```php
// 以 php 为例, 设置一个响应头即可
header('Access-Control-Allow-Origin: 允许请求数据的类型');
// 使用通配符 * ,设置允许全部请求(一般不这么做)
header('Access-Control-Allow-Origin: *');
```

这种方案无需客户端作出任何变化（客户端不用改代码），只是在被请求的服务端响应的时候添加一个 `Access-Control-Allow-Origin` 的响应头，表示这个资源是否允许指定域请求。