## JavaScript简介

### JavaScript是什么

JavaScript是一种***脚本语言*** ，简称JS。

### JavaScript的历史

1995年，由网景公司开发，名叫LiveScript

由于当时Java非常火，LiveScript更名为JavaScript，蹭了一把热度，大火。

Java和JavaScript的关系？

雷锋和雷峰塔，印度和印度尼西亚，周杰和周杰伦，没有任何关系，只是名字很像而已。

### JavaScript最初的目的

最初的目的是为了处理表单的验证操作，提高用户体验。与用户进行交互.

促使其产生的历史环境

   1.网速慢，等待时间长

   2.浏览器并不能在用户提交表单前验证用户输入数据的有效性

   3.如果用户表单中某一项数据填写有误，需要重新填写整个表单，用户体验极差。

### JavaScript如今的应用场景

JavaScript 发展到现在几乎无所不能。

1. 网页特效
2. 服务端开发(Node.js)
3. 命令行工具(Node.js)
4. 桌面程序(Electron)
5. App(Cordova)
6. 控制硬件-物联网(Ruff)
7. 游戏开发(cocos2d-js)
8. 3D(Three.js)

## JavaScript的组成

![1496912475691](media/1496912475691.png)

### ECMAScript

名词解释: ECMA - European Computer Manufacturers Association - 欧洲计算机制造商协会

ECMAScript 是这个组织定义的一套计算机语言规范

JavaScript 是基于这个规范实现的一门计算机脚本语言

规范中描述了该语言的核心基本语法

### BOM 

名词解释: BOM - Browser Object Model - 浏览器对象模型

赋予了JavaScript操作浏览器的能力

通过BOM可以操作浏览器窗口，比如：浏览器历史记录控制、页面跳转、获取分辨率等

### DOM

名词解释: DOM - Document Object Model - 文档对象模型

赋予了JavaScript操作页面元素的能力

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

## JavaScript写法

+ 行内写法(不建议使用)

```html
<input type="button" value="按钮" onclick="alert('Hello World')" />
```

- 写在script标签中
  - 理论来说 **script标签** 可以写在html文档的任何位置

```html
<script>
   <!-- 弹出一个写有 Hello World 文字的弹出框 -->
   window.alert('Hello World');
</script>
```

- 写在外部js文件中，在页面引入

```html
<script src="./main.js"></script>
```

### 细节注意点

- 引用外部js文件的script标签内部不可以写JavaScript代码
- script标签中有type属性和language属性，作用是告诉浏览器当前标签内所写的语言是什么，H5中可以省略不写，浏览器默认的脚本语言是 JavaScript
- 在一个页面中可以有多个script标签，如果某一个script标签中的代码写错了，那么在当前的script标签范围内，错误代码后面的代码就不会执行了，但是不影响后面script标签中代码的执行, 也就是说每一个 script 标签**相当于一个独立的作用域**
- 建议将 script 标签放在 body 结束标签的前面
  - 原因 防止 js 代码优先加载 (js文件默认为同步下载, 执行) 阻塞其他文件的下载和执行, 导致网页可视内容加载的很慢, 影响用户体验

### JavaScript 和 HTML、CSS的基本功能

1. HTML - 结构：组成网页的结构和内容
2. CSS - 表现: 修饰网页
3. JavaScript - 行为: 控制网页内容, 增加动态的效果
4. 特殊:  高版本之后 css 和 js 的界限互相融入
   1. CSS3 之后可以使用某些属性给网页添加动态的效果
   2. JS 也可以使用 DOM 和 HTML-DOM 来修饰网页

## JavaScript运行环境

JavaScript经常运行在浏览器中(不限于浏览器, 用户代理有很多种, 如node.js)，浏览器内置 渲染引擎 和 JavaScript引擎 ，渲染引擎负责**渲染HTML结构和CSS样式**，JavaScript引擎负责**解析并执行JavaScript代码**。

## 计算机组成

### 硬件

- CPU - Central Processing Unit - 中央处理器、内存、硬盘(包括机械硬盘和固态硬盘[SSD])、主板、显卡、声卡、电源、散热器(风冷, 水冷)
- 输入设备：鼠标、键盘、手写板、摄像头、光驱等
- 输出设备：显示器、打印机、投影仪、耳机等

![1497317567484](media/1497317567484.png)

### 软件

- 应用软件：浏览器(Chrome/IE/Firefox)、QQ、Sublime、Word
- 操作系统软件：Windows、Linux、mac OSX、Unix

计算机中的应用软件存储在硬盘中，但是运行的时候会被计算机放在内存中，浏览器也不例外，所以我们写的代码最终都是在内存中执行的。

## 注释

1.对代码进行解释说明 方便自己日后查看 方便同事阅读你的代码

2.在代码调试的过程中 临时注释掉不想执行的代码

### 单行注释

用来描述下面一个或多行代码的作用

```javascript
// 这是一个变量
var name = 'hm';
```

### 多行注释

用来注释多条代码 多行注释不能嵌套使用

```javascript
/*
var age = 18;
var name = 'zs';
console.log(name, age);
*/
```

## 关键字

```js
break
case
catch // 在 try 代码块报错时, 会捕获其中的错误, 如果 try 代码块中有 throw 出的错误则会捕获 throw 出的错误, 并执行一段错误处理代码
  try{代码}catch(err){..代码..console.log(err.message)}
continue
default
delete
do
else
finally // 通常与 try、catch一同使用, 不管try、catch结果如何, 都会执行其中的代码
  finally{代码}
for
function
if
in
instanceof
new
return
switch
this
throw // 一般用在 try 中, 用于抛出异常错误
  try{if(a) throw 'a is not defined'}
try // 运行一段代码, 如果报错就抛出错误, 不会影响代码的继续执行
  try{代码}
typeof
var
void // 该操作符指定要计算一个表达式但是不返回值。
  void(1 + 1)
while
with // 用于设置代码在特定对象中的作用域(浪费性能, 避免使用)
  var obj = {name: 'gt'};
  with(obj) {
    console.log(name); // 'gt'
  }
eval // 将一段字符串作为js代码解析(浪费性能, 避免使用)
 eval('console.log(1)') // 1
```

## 变量

临时存储数据的容器，数据随时可变。

**特殊: 由于 js 是动态的语言所以数据类型也是随时可变的**

### 使用变量

- 只声明不赋值

```javascript
var age;
console.log(age); // 只声明时变量默认值为 undefined 
```

- 声明然后赋值

```javascript
var age;
age = 18;
```

- 同时声明多个变量然后赋值

```javascript
var age, name, sex;
age = 10;
name = 'zs';
```

- 同时声明多个变量并赋值

```javascript
var age = 10, name = 'zs';
```

- 变量名字如果重复, 后面的 var 关键字会被忽略, 相当于变量重新赋值 ( 不建议这样写 )

```javascript
var age = 20;
var age = 30;
console.log(age) // 30
```

+ 特殊

```javascript
var a = b = 10;
// 相当于 
var a = 10; b = 10;
// 无意间创建了一个隐式全局变量b
```

### 变量的命名规则和规范

- 规则( 类似于法律 ) - 必须遵守的，不遵守会报错

  - 由字母(a-z A-Z)、数字(0-9)、下划线_、$符号组成，不能以数字开头
  - 不能是关键字和保留字, 例如：for、while。  但是其中可以包含关键字和保留字
  - 区分字母大小写

- 规范 - 建议遵守的，不遵守不会报错

  - 变量名必须有意义
    - 不要直接用字母当做变量名
    - 如果英语不会，可以用拼音(pinYin)，拼音不要简写(py)，不要拼音和英语混写
  - 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。例如：userName、userPassword


### 变量在内存中的存储

js中的变量和变量值存贮在栈中

```javascript
var age = 18;
```

![1496981558575](media/1496981558575.png)

可以将内存想象成宾馆，宾馆中有若干个房间，每一个房间都会有房间号(内存地址)，比如 0xXXXXXXX1、0xXXXXXXX2、0xXXXXXXX3。由于房间号不好记,

就给房间起一个名字, 这个名字就是变量的名字，房客就是变量的值。

通过房间名可以找到房客----通过变量名字可以找到变量的值。

由于房客可以每天都不一样，这也体现了js变量值可变的特点。

## 数据类型

- 基本数据类型(简单数据类型)
  - number、string、boolean、undefined、null
- 引用数据类型(复杂数据类型)
  - Object、Array、Function、Date、RegExp...

### number类型

- 数值字面量：固定值的表示法
  - 整数:  11
  - 小数(浮点数):  11.1
  - 科学计数法:  5.4e12
- 进制

```
相同点: 
	进行算数计算时，其余进制表示的数值最终都将被转换成十进制数值
	所有进制合法字母不区分大小写
十进制(默认进制)
	var num = 9;
	数字序列范围：0~9
八进制(以0开头)
    var num1 = 07;   // 对应十进制的7
    var num2 = 010;  // 对应十进制的8
    var num3 = 011;   // 对应十进制的9
    数字序列范围：0~7
    特殊: 如果字面值中的数值超出了范围，那么前导零将被忽略，后面的数值将被当作十进制数值解析, 其余进制均为报错
十六进制(以0x开头)
	var num = 0xA;   // 对应十进制的10
	数字序列范围：0~9以及A~F(10-15)  
H5新增
二进制(以0b开头)
 	var num3 = 0b11;   // 对应十进制的3
    数字序列范围：0~1
八进制(以0o开头)
	同上八进制
```

- 浮点数(小数)

```
// 浮点数在运算的时候得到的结果是不准确的
var result = 0.1 + 0.2;     // 结果不是 0.3，而是：0.30000000000000004
console.log(result == 0.3); // false 
注意: 永远不要判断两个浮点数是否相等

// 解决办法
// 将浮点数升级成整数 再将运算结果降级
var result = (0.1*10 + 0.2*10)/10; // 0.3

// es6 引入了 Number.EPSILON 常量
引入这么小的一个常量的目的在于，为浮点数计算设置一个误差范围。因为浮点数的计算是不精确的。如果误差小于Number.EPSILON, 我们就可以认为得到了正确的结果
```

- 数值范围

```
最小值：Number.MIN_VALUE，这个值为： 5e-324
最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
无穷大：Infinity  // 大于最大值为无穷大
无穷小：-Infinity // 小于最小值为无穷小
```

- NaN：not a number

  - NaN 本身是一个数字类型

  - NaN 与任何值都不相等，包括他本身

    ```javascript
    console.log(undefined + 10); // NaN
    console.log(typeof NaN) // number
    console.log(NaN === NaN) // false
    ```

- isNaN(变量/值): 判断是否不是一个数字，如果不是数字，结果就是true，如果是数字，结果就是false

  ```javascript
  isNaN(undefined + 10) // true
  ```

  + 注意存在隐式转换

    ```javascript
    // 会将其中的数据尝试转换成数字类型, 然后进行判断
    // 例如: 纯数字字符串, true(1), false(0), null(0)
    isNaN('1') // false
    ```

### string类型

- 字符串定义

  ```javascript
  // 使用单双引号都可
  var str1 = '程序猿';
  var str2 = "程序媛";
  // 特殊字符可使用转义符号进行转义
  var str3 = 'ni\"shi'; 
  ```

- 转义符

  ![1498289626813](media/1498289626813.png)

- 字符串长度

  length属性用来获取字符串的长度

  ```javascript
  var str = '黑马 程序猿';
  console.log(str.length); // 6
  ```

- 字符串拼接

  + 字符串拼接使用 + 连接
  + 特殊: 两个包含着完全相同的字符并且字符排列书序也相同的两个字符串是完全相同的 
    + 例如:   "a"+"bc" === "abc"  // true

  ```javascript
  console.log('hello' + ' world');  // 'helloworld'
  console.log('11' + 11);           // '1111'
  console.log('male:' + true);      // 'maletrue'
  console.log(11 + 11);             // 22
  ```

  1. 两边只要有一个是字符串，那么 + 就是字符串拼接功能
  2. 两边如果都是数字，那么就是算术功能。

- 字符串注意事项

  - 用单引号或双引号定义的字符串必须一行显示，中间不能有回车或换行符。
  - 单双引号只能互相嵌套使用, 也就是说双引号之中不能包含双引号 ，单引号之中不能包含单引号，若一定要包含，使用转义字符。

### boolean类型

- Boolean字面量：  true 和 false，区分大小写(不能使用大写)

### undefined 

undefined表示"未定义的"，就是此处应该有一个值，但是还没有定义，典型用法是：

- 变量声明了，但没有赋值时，就等于undefined

- 调用函数时，实参少于形参时，多余的形参为undefined

- 对象定义了但是没有赋值的属性，该属性的值为undefined

- 访问数组中不存在的值，返回undefined

- 函数没有返回值时，默认返回undefined

  ```javascript
  function add(x, y) {
    var sum = x + y;
    // 情况一 没有return
    // 情况二 有return 无返回值
    return; 
    // 情况三 return 和 返回值 没在同一行
    return  // 相当于在此行最后自动添加 ; 分号
    100;    
  }

  var result = add(10, 20);
  console.log(result);  // undefined
  ```

### 获取变量/值的类型

typeof 关键字   或者  函数写法   typeof(变量/值)

+ 一共6种返回值, 返回值为字符串全小写格式 
  + 'number' , 'string' , 'boolean' , 'object' , 'function' , 'undefined'
    + 特殊:  null, 数组属于 object 类型
  + es6之后 新增第7个值 'symbol' 唯一标识符类型(简单类型)
    + var str = Symbol('str');   typeof  str;   //   'symbol'

```javascript
var age = 18;
console.log(typeof age);  // 'number'
```

+ 谷歌浏览器控制台快速的查看数据类型
  + 字符串的颜色是黑色的，数值类型和布尔类型是蓝色的，undefined和null是灰色的

### null

+ 特殊值: 表示空, 只能为小写格式
+ **一般情况下都不可能为 null 值**; DOM核心方法获取元素对象获取不到时, 返回null;
+ 可以将变量手动赋值为 null, 表示为可以清除此变量

## 数据类型转换

```javascript
// prompt 返回的数据为字符类型
var num1 = prompt("请输入第一个数字");
var num2 = prompt("请输入第二个数字");
var num3 = num1 + num2;
alert("结果是" + num3);
```

### 转换成数值类型

通用: 会忽略第一个非空格字符前面的所有空格, 可以识别正负符号(+ -)

- Number()

  ```javascript
  // 严格转换数字类型, 如果要转换的字符串中含有不是数值的字符(不包括唯一一个.) 返回NaN
  Number('1.1');   // 100
  Number('1.1.1'); // NaN
  Number('1a2');   // NaN
  // 可以识别科学计数法, e不区分大小写
  Number('1e2');   // 100
  ```

- parseInt()

  ```javascript
  // 如果第一个字符是数字会解析直到遇到非数字结束
  var num1 = parseInt("12.3abc");  // 12
  // 如果第一个字符不是数字或者符号(+ -)就返回 NaN
  var num2 = parseInt("abc123");   // NaN
  ```

- parseFloat()

  ```
  把字符串转换成浮点数或者整数
  使用方法同 parseInt()
  特殊:	parseFloat()会解析第一个. 遇到第二个.或者非数字结束
  ```

- 隐式类型转换

  - 没有明确告诉JavaScript进行数据类型转换，但是程序在运行的过程中自动的进行了数据类型的转换

  ```javascript
  var str = '500';
  console.log(str - 10); // 490
  ```

### 转换成字符串类型

- 变量/(值).toString([进制])

  - 进制为数字类型  范围为 2 - 36 进制, 默认为10进制

  ```javascript
  var num = 5;
  console.log(num.toString()); // '5'
  ```

- String(变量 / 值)

  ```javascript
  String()函数存在的意义：有些值没有toString()，这个时候可以使用String()。比如：undefined 和 null
  ```

- 拼接字符串方式

  ```
  num  +  ''; 当 + 两边一个操作符是字符串类型，一个操作符是其它类型的时候，会先把其它类型转换成字符串再进行字符串拼接，返回字符串
  ```

### 转换成布尔类型

- Boolean(变量 / 值)
  + 除了以下值, 其他值都会转换成 true
    + (+)0, -0, ''(空字符串), false, undefined, null
- 隐式转换为布尔类型
  - 在 if , else if, 判断和比较中都会将值隐式转换为布尔类型进行比较