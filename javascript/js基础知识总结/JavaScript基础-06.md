## 基本类型和引用类型的区别

- 基本数据类型
  - number、string、boolean、undefined、null
- 引用数据类型
  - object array function

```javascript
// 基本数据类型
var a = 10;
var b = a;
a = 20;
console.log(b);

// 引用数据类型
var obj1 = {
    name: "张三";
}
var obj2 = obj1;
obj1.name = "李四";
console.log(obj2.name);

// 基本数据类型
var num = 20;
function fn(num){
    num = 30;
    console.log(num);
}
fn(num);
console.log(num);

// 引用数据类型
var obj = {
    name: "张三"
}
function fn(arg){
    obj.name = "李四";
}
fn(obj);
console.log(obj);
```

基本类型：在存储时，变量中存储的是值本身，因此也叫做值类型。

引用类型：在存储时，变量中存储的仅仅是地址。

堆和栈

```
堆栈空间分配区别：
　　1、栈：存储基本数据类型的值 代码运行
　　2、堆：存储引用数据类型的值
　　3、堆比栈大 栈比堆快
```
注意：JavaScript中没有堆和栈的概念，此处我们用堆和栈来讲解，目的方便理解和方便以后的学习。

### 基本类型在内存中的存储

![1498288494687](media/1498288494687.png)

### 引用类型在内存中的存储

![1498700592589](media/1498700592589.png)

### 基本类型作为函数的参数

![1497497605587](media/1497497605587-8288640195.png)

### 复杂类型作为函数的参数

![1497497865969](media/1497497865969.png)

```javascript
// 下面代码输出的结果
function Person(name,age,salary) {
  this.name = name;
  this.age = age;
  this.salary = salary;
}
function f1(person) {
  person.name = "ls";
  person = new Person("aa",18,10);
}

var p = new Person("zs",18,1000);
console.log(p.name); // zs
f1(p);
console.log(p.name); // ls
```

思考：

```javascript
//1. 
var num1 = 10;
var num2 = num1;
num1 = 20;
console.log(num1);
console.log(num2);

//2. 
var num = 50;
function f1(num) {
    num = 60;
    console.log(num);
}
f1(num);
console.log(num);

//3. 
var num1 = 55;
var num2 = 66;
function f1(num, num1) {
  num = 100; // 局部
  num1 = 100; // 局部
  num2 = 100; // 全局
  console.log(num); // 100
  console.log(num1); // 100
  console.log(num2); // 100
}

f1(num1, num2);
console.log(num1); // 55
console.log(num2); // 100
console.log(num); // num is not defined
```

## 数据类型判断

- typeof  返回变量的类型，只能区别出基本数据类型和函数，不能区别出对象和数组

  ```javascript
  var str = "abc";
  console.log(typeof str);

  var number = 12;
  console.log(typeof number);

  var bool = true;
  console.log(typeof bool);

  var func = function() {};
  console.log(typeof func);

  var obj = {};
  console.log(typeof obj);

  var arr = [];
  console.log(typeof arr);
  ```

- instanceof 判断实例是否属于某个构造器

  ```javascript
  var obj = {};
  var arr = [];

  console.log(obj instanceof Object); // true
  console.log(arr instanceof Array);  // true

  function getDataType(o) {
      if (o instanceof Array) {
          return "array";
      } else if (o instance Object) {
          return "object";
      }else {
          return "参数不是对象或者数组";
      }
  }

  // instance 通常不用来判断基本数据类型
  ```

  以上判断数据类型的方式都不是最优的，随着以后知识点的不断深入学习，会有更加好的方法。

## window对象

window对象表示浏览器窗口。

- 全局变量是 window 对象的属性
- 全局函数是 window 对象的方法。
- 甚至 HTML DOM 的 document 也是 window 对象的属性之一

```javascript
var num = 20;
console.log(window.num); // 相当于给window对象添加了一个属性num,值是20

function fn () {
    console.log("fn函数相当于是window对象下面的一个方法");
}

// 在平时使用的使用 window对象可以省略不写
window.fn();
window.alert("alert是window对象下面的方法");
window.prompt("prompt是window对象下面的方法");

console.log(window.innerHeight); // 浏览器窗口的内部高度
console.log(window.innerWidth); // 浏览器窗口的内部高度
window.open("http://www.baidu.com"); // 打开新窗口
```

## this关键字

this在js中是一个特殊的对象，在程序运行的过程中，this的指向随时可变。

在全局作用域下输出this，指向window对象，所以我们主要研究的是函数中的this。

JS中的this是指当前行为执行的主体。

```javascript 
function 吃饭 () {
    console.log(this); // 班长
}
班长.吃饭();
```

函数内部的this几个特点

```
1. 函数在定义的时候this是不确定的，只有在调用的时候才可以确定
2. 函数执行，首先看函数前面是否有"."，有话的，"."前面是谁，函数中的this就是谁，没有的话，this就是window
3. 自执行函数中的this永远是window
4. 构造函数中的this其实是一个隐式对象，所有方法和属性都挂载到了这个隐式对象身上，后续通过new关键字来调用，从而实现实例化
5. this是谁只和它的执行主体有关系 和函数在哪定义 在哪执行没有任何关系
```

```javascript
function fn () {
    console.log(this);
}
var person = {
    fn: fn
}

fn(); // window
person.fn(); // person

function sum () {
    console.log(this)
    fn(); // window
}
sum();  // window

var obj = {
    sum : function(){
        console.log(this);
        fn(); // window
    }
}
obj.sum(); // obj
```

```javascript
var person = {
    name: '张三',
    age: 20,
    say : function(){
        console.log(this);
    }
}
person.say(); // person
var speak = person.say;
speak(); // window
```

```javascript
(function(){
    console.log(this);
})()
```

```javascript
function CreatePerson (name, age) {
    this.name = name;
    this.age = age;
    console.log(this);
}

CreatePerson();

var p1 = new CreatePerson("zhangsan", 20);
```

## 伪数组

伪数不是数组，虽然可以以数组的方式获取其中的元素，但是不可以调用数组下面的方法。

伪数组是一种特殊格式的对象，按索引方式存储数据，且拥有length属性，length属性是数值类型。

```javascript
var likeArray = {
    0: 'a',
    1: 'b',
    2: 'c',
    length: 3
}
```

- arguments
- new String("str")
- getElementsByTagName()