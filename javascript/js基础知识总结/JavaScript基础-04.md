## 作用域

作用域：变量可以起作用的范围

### script 元素的作用域

```html
<script>
  console.log(i); //在上script标签中为报错未定义
</script>
<script>
  console.log(i); // 在当前 script 标签中为undefined
  for (var i = 0; i < 9; i++) {

  }
  console.log(i);// i=9
</script>
<script>
  console.log(i);// 在下script标签中为9
</script>
```

```html
/**
*不同script标签中的同名函数不互相影响
*第二个函数相当于重新赋值
*/
<script>
  function f1() {
    console.log("哇塞");
  }

  f1();//哇塞
</script>
<script>
  f1();//哦买噶的

  function f1() {
    console.log("哦买噶的");
  }
</script>
```

### 全局作用域和局部作用域

- 全局作用域
  + 供所有代码执行的环境
- 局部作用域（函数作用域）
  + 由于 es6 之前没有块级作用域(就是 { } 作用域), 所以局部作用域只有函数作用域
  + 在调用函数的时候，函数内部会形成一个私有的封闭的环境。
- 全局作用域是默认就有的，局部作用域是函数在执行的时候创建的，也只有函数可以创建局部作用域。
- 浏览器不关闭, 全局作用域不会消失; 函数执行完成之后, 局部作用域消失.

### 全局变量和局部变量

- 全局变量

  - 在全局作用域下声明的变量叫做全局变量（在函数外部定义的变量）
  - 全局变量在代码的任何位置都可以使用(声明该全局变量script标签中及其下面的script标签)
  - 全局变量不可以使用 delete 删除

- 隐式全局变量

  - 由于没有 var 关键字, 所以不存在变量提升, 所以只有在定义之后才可以使用.

  - 隐式全局变量可以使用 delete 删除

  - 在变量定义时没有使用关键字 var 就可能会产生隐式全局变量

    ```js
    // 第一种情况
    a = 1;
    // 第二种情况
    function () {
      a = 1;
    }
    ```

  - 在使用自定义构造函数创建实例时, 没有使用 new 关键字也会产生隐式全局变量

    ```js
    // 定义一个构造函数
    function Fn() {
      this.a = 1;
    }
    // 无意间创造了 a 隐式全局变量, 没有改变 this 指向, 默认指向window
    var fn = Fn();
    ```

- 局部变量

  - 在局部作用域下声明的变量叫做局部变量（在函数内部定义的变量）
  - 局部变量不可以使用 delete 删除
  - 局部变量只能在该函数内部使用

```javascript
var scope = 12; // 全局变量
function demo() {
    var local = 1; // 局部变量
    console.log(scope) // 12
    console.log(local) // 1
}
console.log(scope) // 12
console.log(local) // 报错 local is not defined
```

### 变量释放

- 全局变量会在浏览器关闭后销毁
- 局部变量在函数执行完毕之后立即销毁

### 垃圾回收机制

### 作用域嵌套

不同的作用域下声明的变量是不会发生冲突的。

```javascript
var scope = "global";
function fn1(){
    var scope = "local-a";
    function fn2(){
        var scope = "local-b";
    }
}
```

### 作用域链

```javascript
var scope = "global";
function CheckScope(){
    return scope;
}
// 函数返回的 scope 值为全局作用域中的 scope
// 首先会在当前函数作用域中查找, 如果没有会去上一级查找, 如果还是没有就在往上一级查找, 直到全局作用域
CheckScope();
```

在作用域嵌套的情况下，函数内部用链式查找的方式访问函数外部的变量，称作作用域链。

作用域链只能从内向外查找，不能从外向内查找，采用就近原则。

## js解析器

JavaScript代码是由浏览器中的JavaScript解析器来执行的。JavaScript解析器在运行JavaScript代码的时候，分为两步：预解析和代码执行

### 预解析

```
//预解析:在解释代码之前发生的事情 !!!!从上到下依次预解析!!!!
//变量的预解析:在使用这个变量的时候,会把变量的声明提前到当前所在域(script标签)的最上面,赋值不会提前.这个过程就叫变量的预解析
//函数的预解析:在调用这个函数的时候,会把该函数的声明(赋值和调用不会提前)提升到当前所在域的最上面,这个过程,叫函数的预解析
//预解析的时候,函数中的局部变量的声明会提升到当前函数作用域里面的最上面,不会提升到其他的作用域中
//预解析的时候,如果有多对的script标签,那么如果函数名相同,预解析的时候相互之间不会受到影响的(下面的 script 的函数相当于变量的重新赋值)
```

```javascript
// 案例1
console.log(num); // undefined
var num = 10;
function fn(){
    console.log(num); // undefined
    var num = 20;
    console.log(num); // 20
} 
fn();

// 案例2
var num = 10;
fun();
function fun() {
  console.log(num); // undefined
  var num = 20;
}

// 案例3
var a = 18;
f1();
function f1() {
  var b = 9;
  console.log(a); // undefined
  console.log(b); // 9
  var a = '123';
}

// 案例4
var a = 25;
function abc (){
  console.log(a); // undefined
  var a = 10;
}
abc();
console.log(a); // 25
function a() {
  console.log('aaaaa');
}
var a = 1;
console.log(a); // 1

// 案例5
f1();
console.log(c); // 9
console.log(b); // 9
console.log(a); // 报错 a is not defined
function f1() {
  // 相当于 var a = 9; b = 9; c = 9;
  var a = b = c = 9;
  console.log(a); // 9
  console.log(b); // 9
  console.log(c); // 9
}
```

预解析也叫做变量、函数提升

- 变量提升

  定义变量的时候，变量的声明会被提升到当前作用域的最上面，变量的赋值不会提升。

- 函数提升

  JavaScript解析器会把当前作用域的函数声明提前到整个作用域的最前面

  ```javascript
  // 练习 1
  console.log(a) // undefined
  console.log(fn) // function fn(){ return false; }

  var a = 1;
  function fn(){ 
      return false;
  };

  // 练习2
  var a; 
  function fn(){
      return false;
  }; 

  console.log(a); // undefined
  console.log(fn); // function fn(){ return true; }
  a = 1; 
  function fn(){ 
      return true;
  };

  // 练习3
  console.log(a); // function a(){ return false; }
  var a = 1;
  console.log(a); // 1
  function a(){
      return false;
  }
  ```

### 代码执行

代码执行阶段发生在预解析之后, 按照预解析之后的代码进行`从上到下, 从左到右`的顺序依次执行

## 对象

对象是JavaScript中最重要的数据类型，可以让数据存储的更加形象化。

```javascript
// 分别用基本数据类型（字符串、数字、布尔）、数组、对象表示一个人的信息
// 基本数据类型
var name = "zhangsan";
var age = 20;
var isMarry = false;

// 数组
var people = ['张三', 20, false];

// 对象
var person = {
    name: 'zhangsan',
    age: 20,
    isMarry: false
}
```

### 什么是对象

```
现实生活中：万物皆对象，对象是一个具体的事物。
	举例： 车，手机
	车是一类事物，门口停的那辆车才是对象
一个具体的事物就会有行为和特征
	特征：红色、四个轮子
	行为：驾驶、刹车
```

### JavaScript中的对象

- 在JavaScript中，如何描述生活中的对象?
  - JavaScript对象就是用来描述生活中的对象的。
- JavaScript对象有什么特点呢？
  - JavaScript对象是无序属性的集合。
  - 属性的值可以是任意Javascript数据类型值
  - 对象的行为通常用函数表示
  - 对象的特征通常用非函数表示

### 对象创建方式

- 对象字面量

```javascript
var o = {
  name: 'zs',
  age: 18,
  sex: true,
  sayHi: function () {
    console.log(o.name);
  }
};   
```

- new Object()创建对象

```javascript
var person = new Object();
person.name = 'lisi';
person.age = 35;
person.job = 'actor';
person.sayHi = function(){
    console.log('Hello,everyBody');
}
```

​	以上创建对象方式的弊端

​		1.批量创建对象代码重复

​		2.不能分辨出具体是哪一个对象

​	以上创建对象方式的使用场景

​		1.在程序运行的过程中，临时存储数据。

​		2.充当命名空间，防止代码冲突覆盖

```javascript
var zhangsan = {}；
zhangsan.a = 10;
var lisi = {};
lisi.a = 20;
```

- 工厂模式

```javascript
function createPerson(name, age, job) {
  var person = new Object();
  person.name = name;
  person.age = age;
  person.job = job;
  person.sayHi = function(){
    console.log('Hello,everyBody');
  }
  return person;
}
var p1 = createPerson('张三', 22, 'actor');
```

- 自定义构造函数模式
  - 在JavaScript中，用构造函数描述具有相同特征的一类事物，可以用自定义构造函数创建属于这一类事物的公用父对象。
  - `使用自定义构造函数时, 一定要带 new 关键字, 否则自定义构造函数的this就会错误的指向window, 并创建出多余的隐式全局变量`

```javascript
function Person(name,age,job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayHi = function(){
  	console.log('Hello,everyBody');
  }
}
var p1 = new Person('张三', 22, 'actor');
```

### new关键字

> 构造函数 ，是一种特殊的函数。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建实例化对象的语句中。

1. 构造函数用于创建一类对象，首字母建议大写。
2. 构造函数通常与 new 一起使用.

new在执行时会做四件事情

```
1. 在内存中创建一个新的空对象
2. 让this指向这个新的对象
3. 执行构造函数  目的：给这个新对象加属性和方法
4. 返回这个新对象
```

Object 是系统内置的构造函数，所以可以使用new关键字。

### 构造函数与普通函数的区别

- 构造函数首字母大写（约定俗成）
- 目的不同，普通函数是调用，做一些事情，构造函数是为了创建实例对象。

## 对象的使用

### 获取对象属性的另一种方式

```javascript
var person = {
    name: 'zhangsan',
    age: 20
};
console.log(person.name); // 'zhangsan'
console.log(person['name']); // 'zhangsan'
```

### 遍历对象

将对象中每个属性所对应的值取出来

> 通过for..in语法可以遍历一个对象

```javascript
for(var key in obj){
    console.log(obj[key]);
}
```

### 删除对象属性或方法

```javascript
function Fun() { 
  this.name = 'mm';
}
var obj = new Fun(); 
console.log(obj.name); // mm 
delete obj.name;
// 虽然 name 属性被删除了, 但是.name之后又有了此属性, 相当于定义未赋值, 所以是 undefined
console.log(obj.name); // undefined
```

### 判断对象中没有没某一个属性或方法

```javascript
var obj = {
    name: "张三",
    age: 20,
  	eat: function () {}
}

if(obj.name){
   console.log("有");
}else{
    console.log("没有");
}

if(obj["age"]){
    console.log("有");
}else{
    console.log("没有");
}

if("age" in obj){
	console.log("有");
}else{
 	console.log("没有");
}

if (obj.hasOwnProperty('eat')) {
	console.log("有");
} else {
	console.log("没有");
}
```

### null 特殊值

null 和 undefined 都表示“值的空缺”，你可以认为undefined是表示系统级的、出乎意料的或类似错误的值的空缺，而null是表示程序级的、正常的或在意料之中的值的空缺。

null表示空对象指针。

变量的值如果想为null，必须手动设置; 想清除变量时, 一般将其赋值为 null

DOM核心获取元素对象方法获取不到时, 返回null;

```js
typeof null // object
```