### let与const

```
let 定义变量 可以只声明 不赋值
const 定义常量 声明时必须赋值 一旦定义不可轻易改变值 (由于复杂类型存贮的是引用, 所以改变对象的成员不会报错, 不建议这样做)
解决 var 没有块作用域, 变量提升, 可以重复声明 的问题
let 和 const 有自己的块作用域, 不存在变量提升问题, 同一块作用域中不可重复声明(会报错)

let, const 暂时性死区问题
在块作用域中 只要有let/const声明的变量 在未声明之前使用或者赋值都会报错 相当于let/const声明的变量霸占了此区域 
var tmp = 123;
if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}

let 和 const 定义的变量和常量 不能添加到 window 中
```



### 字符串的扩展

```
var str = 'qwe asd' 
判断是否包含某字符串
str.includes('qwe') // true
判断是否为某字符串开头
str.startsWith('qwe') //true
判断是否为某字符串结尾
str.endsWith('asd') //true
重复拼接某字符串
str.repeat(3) // 'qwe asdqwe asdqwe asd'
在字符串的前面添加前缀, 返回添加之后的字符串
str.padStart(拼接之后的总长度, 要在前面拼接的字符串)
eg: '1'.padStart(2, '0') // '01'
在字符串的后面添加前缀, 返回添加之后的字符串
str.padEnd(拼接之后的总长度, 要在后面拼接的字符串)
```



### 数组的扩展

```
Array.from(伪数组)    将一个伪数组转换成数组  返回值为数组
Array.of(若干个值 undefined 等特殊类型值也可)    将其变成数组的形式返回  返回值为数组
数组.find((item,index,arr) => {条件})    返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。
数组.findIndex((item,index,arr) => {条件})    返回数组中满足提供的测试函数的第一个元素的索引值。否则返回 undefined。
数组.includes(数据,[searchIndex])   判断数据是否在数组中,第二个参数(可选参数)为从指定索引处(包含索引处的值)开始搜索  返回布尔值(es7时加入)

```



### 解构赋值

```
前后的形式必须完全一致 才可以完成结构赋值

数组
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
如果解构不成功，变量的值就等于undefined。

对象
对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
{name, age} = {name:'wang',age: 18}
name // wang
age // 18

支持别名
{name:nname, age} = {name:'wang',age: 18}
name // '' 取别名时原名就会为空字符串
nname // wang
age // 18

==================以下为对象和数组均可======================
不完全解构
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4

默认值
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
注意，ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。

默认值可以引用解构赋值的其他变量，但该变量必须已经声明。
let [x = 1, y = x] = [];     // x=1; y=1
let [x = 1, y = x] = [2];    // x=2; y=2
let [x = 1, y = x] = [1, 2]; // x=1; y=2
let [x = y, y = 1] = [];     // ReferenceError

...运算符
[a, ...b] = [1,2,3,4,5]
a // 1
b // [2,3,4,5]

var app = (...sum) => {sum.forEach(item => console.log(item) )}
app(1,2,3,4) // 1,2,3,4
此运算符或得值为数组形式 主要用于替代函数中的 arguments(伪数组) 属性 这样可以非常方便的遍历获取到的未知个数的实参

特殊使用方法
// fs 模块导出一个接口对象
// 接口对象中是不是有 readFile 这个方法成员
var {readFile, writeFile} = require('fs')

readFile('./tpl.html', 'utf8', function (err, data) {
  if (err) {
    throw err
  }
  console.log(data)
})
```



### 模板字符串

``` 
使用 ` 字符包围的字符串 其中可使用并会保留换行 空格等操作(类似于 pre 标签) 可使用 $(变量名) 来解析包含其中的变量
var obj = {name:'wang',age:18}
var str = `
我叫$(obj.name),
今年$(obj.age)岁了
`
我叫wang,
今年18岁了
```



### 箭头函数

```
箭头函数，本质上，就是一个匿名函数

函数支持默认值
function add(x = 10, y = 20) {
  console.log(x, y)
}
add(20) // 20, 20

箭头函数
单个参数可以省略 () ;无 {} 时执行语句自动添加 return 不能显示写 return,否则报错;单句执行语句可以省略 {}
=> 读作 goes to 去做
var app = x => x
var app = (x, y) => x + y
var app = (x, y) => {return x + y}
注意 : 箭头函数不能当作构造函数

!!!!!!!!!!this问题!!!!!!!!!!
箭头函数无法通过 call、apply、bind 来手动改变内部 this 指向
箭头函数：自动 .bind(this)  也就是说箭头函数中的this指向与其所在作用域的this指向相同

函数在对象中的简写
{函数名 ([参数]) {函数体} }
例 : {add(x, y) {return x + y}}

对象名在对象中的简写
当 键 和 值 名相同时可以只用键声明
{data: data} 可以写成 {data}
```



### for循环作用域

~~~
for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
~~~



### 指数运算符

```
n ** m 计算指数运算  n 的 m 次幂, 与 Math.pow() 行为一致
存在隐式转换, 字符串会强制转换成数字进行运算, 计算失败返回NaN
2 ** 3 // 8
'2' ** 3 // 8
's' ** 3 //NaN
```

