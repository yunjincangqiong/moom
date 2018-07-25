## 内置对象

JavaScript中的对象分为3种：内置对象、本地对象、宿主对象

### [MDN](https://developer.mozilla.org/zh-CN/)权威学习文档



### Date - 日期时间

#### 获取当前日期

以下返回值都是 number 类型, 除 年外 , 其余获取的值个位数时都没有前导0

```javascript
// 创建实例化日期对象
var dt = new Date();
// 获取4位数的年份
var YYYY = dt.getFullYear();
// 获取月份（从零开始）
var MM = dt.getMonth();
// 获取天数
var DD = dt.getDate();
// 获取星期几 0是周日 1是周一 ...
var week = dt.getDay();
// 获取小时
var HH = dt.getHours();
// 获取分钟
var mm = dt.getMinutes();
// 获取秒
var ss = dt.getSeconds();
```



#### 设置日期

```javascript
// 方法一  设置具体的时间 年, 月（月份从0开始）, 日, 时, 分, 秒 
var dt = new Date(2015, 4, 1, 3, 24, 0);
// 方法二  设置时间戳
var dt = new Date(1453094034000);
```



#### 获取日期毫秒数(时间戳)

以下方法返回值全为 number 类型

```javascript
// 时间戳：当前距1970年1月1日 0时0分0秒（世界标准时间）的毫秒数
var dt = new Date();
// 方法一
console.log(dt.valueOf());
// 方法二(常用)
console.log(dt.getTime());
// 方法三(常用)
console.log(Date.now());
// 方法四
console.log(+ new Date());
```



#### 秒换算公式

```
天：Math.floor(t/86400)
时：Math.floor(t%86400/3600)
分：Math.floor(t%86400%3600/60)
秒：Math.floor(t%60)
```



#### 案例

- 写一个函数，格式化日期对象，返回 YYYY-MM-DD HH:mm:ss 的形式

```javascript
function formatDate(d) {
  // 如果date不是日期对象，返回
  if (!(date instanceof Date)) {
    return;
  }
  var year = d.getFullYear(),
      month = d.getMonth() + 1, 
      date = d.getDate(), 
      hour = d.getHours(), 
      minute = d.getMinutes(), 
      second = d.getSeconds();
  month = month < 10 ? '0' + month : month;
  date = date < 10 ? '0' + date : date;
  hour = hour < 10 ? '0' + hour : hour;
  minute = minute < 10 ? '0' + minute:minute;
  second = second < 10 ? '0' + second:second;
  return year + '-' + month + '-' + date + ' ' + hour + ':' + minute + ':' + second;
}
```

- 计算时间差，返回相差的天/时/分/秒

```javascript
// 参数: 未来的时间
function getTimeDifference (future) {

    // 将来的时间
    var futureTime = future.getTime();

    // 现在的时间
    var nowTime = new Date().getTime();

    // 时间差毫秒数
    var difference = futureTime - nowTime;

    // 时间差秒数
    var seconds = difference / 1000;

    // 把当前时间差换算为天, 时, 分, 秒
    var day = Math.floor(seconds/86400)
    var hours = Math.floor(seconds%86400/3600)
    var minutes = Math.floor(seconds%86400%3600/60)
    var second = Math.floor(seconds%60);

    // 返回计算之后的时间差
    return {
        day: day,
        hours: hours,
        minutes: minutes,
        second: second
    }
    
}

var time = getTimeDifference(new Date(2008, 8, 8, 8, 8, 8));

console.log(time);
```



### Array - 数组

#### 创建数组的两种方式

```javascript
// 1. 使用字面量创建数组对象
var arr = [1, 2, 3];

// 2. 使用构造函数创建数组对象
// 创建了一个空数组
var arr = new Array();
// 创建了一个数组，里面存放了3个字符串
var arr = new Array('zs', 'ls', 'ww');
// 创建了一个数组，设置数组的长度为5, 每个值都为 undefined
var arr = new Array(5);
```



#### 判断是否为数组

+ Array.isArray(arr) 静态方法, 判断是否为数组, 返回的是布尔类型(高版本浏览器支持)
         + arr instanceof Array 返回布尔类型的值
         + arr.constructor === Array 返回布尔类型的值
         + Object.prototype.toString.call(arr) 看返回值是否是 '[Object Array]'(字符串类型)



#### 数组常用方法

#### 以下方法会改变原数组的值

##### push()

+ 向数组后追加数据(多个数据用逗号隔开), 返回值是追加数据后的数组的长度
+ arr.push(数据)

##### unshift()

+ 向数组中第一个元素前插入数据(多个数据用逗号隔开), 返回值是插入数据后数组的长度
+ arr.unshift(数据)

##### shift()

+ 删除数组中的第一个数据, 返回值是删除的那个数据
+ arr.shift()

##### pop()

+ 删除数组中的最后一个数据, 返回值是删除的那个数据
+ arr.pop()

##### splice()

+ 从指定的位置开始删除指定个数的数据, 然后添在当前位置添加数据, 返回值为 由被删除的数据组成的一个数组`(没有删除数据返回空数组)`。
+ .splice(start, deletecount, item1, item2...)
  + start :指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从-1计数）
  + deletecount(可选) : 整数，表示要移除的数组元素的个数。
           * 如果 deleteCount 是 0，则不移除元素。这种情况下，至少应添加一个新元素。
           * 如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。
           * 如果deleteCount被省略，则其相当于(arr.length - start)。也就是相当于包含start位置及其后的所有数据
         + items(可选) : 要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。

##### reverse()

+ 反转当前数组数据, 返回值为反转之后的数组
+ arr.reverse()

##### sort()

+ 数组排序,默认为从小到大排序,按照ASCII码值排序 对字母数组进行排序是直调用即可
+ arr.sort(callback)
  + 正向排序回调函数为
    ​         function (a, b) {
    ​            return a - b;
    ​            // return ~~(a > b); 
    ​         }
  + 反向排序回调函数为
    ​         function (a, b) {
    ​            return b - a;
    ​            // return ~~(a < b);
    ​         }



#### 以下方法不改变原数组的值

##### concat()

+ 在原数组后连接数组数据, 返回值为连接后的新数组
+ arr.concat(数组数据, ...)

##### slice()

+ 截取数组中的数据, 返回新的数组, 包含开始索引位置处的值, 不包含结束索引处的值
+ arr.slice(开始索引,结束索引)
  + 无参数是为截取全部数据
  + 只有前一个参数时, 从指定位置截取到最后

##### indexOf()

+ 在数组中查找第一个匹配的值, 并返回其的索引, 找不到返回 -1
+ arr.indexOf(要查找的数据, 开始查找位置的索引)
  + 第二个参数为可选参数, 返回结果包含指定位置处的索引

##### lastIndexOf()

- 在数组中倒叙查找(从右往左)第一个匹配的值, 并返回其的索引(为正着数的索引), 找不到返回 -1
- arr.lastIndexOf(要查找的数据, 开始查找位置的索引)
  - 第二个参数为可选参数, 最后一个值的索引为-1, 倒数第二个值为-2, 以此类推, 返回结果包含指定位置处的索引

##### join()

+ 把数组每个元素中间加上一个连接符(字符串格式), 返回值为拼接之后的`字符串`
+ **如果数组的任一元素为 undefined 或 null，使用join方法时该元素将被视为空字符串。**
+ arr.join('-')

以下五个方法都有一个回调函数作为参数, 并且每个回调函数都有三个可选参数, 第一个参数为 数组的每一项的值, 第二个参数为 对应的数组的每一项的索引, 第三个参数为 数组本身

##### forEach()

+ 遍历数组, 无返回值(默认返回undefined)

以下方法都需要 return 数据

##### filter()

+ 返回符合回调函数条件的数据组成的新数组
+ arr.filter((v) => {return v > 5})  
  + 返回所有值大于5的数据组成的数组

##### every()

+ 每个元素都要满足条件才返回true, 反之返回 false
+ arr.every((v) => {return v > 5})
  + 如果所有值都大于5返回true

##### some()

+ 至少有一个元素满足条件才返回true, 反之返回 false
+ arr.some((v) => {return v > 5})
  + 如果有任何一个值大于5返回true

##### map()

+ 每个元素都要执行一次回调函数, 返回操作后的数据组成的数组
+ arr.filter((v) => {return v + 5})
  + 每个数据加5之后返回新的数组



清空数组

```javascript
// 方式1 推荐 
arr = [];
// 方式2 
arr.length = 0;
// 方式3
arr.splice(0, arr.length);
```



#### 案例

- 将一个字符串数组输出为|分割的形式，比如“刘备|张飞|关羽”。

```javascript
var ary1 = ["刘备", "张飞", "关羽"]; // 刘备|张飞|关羽
var str = "";
ary1.forEach(function(element,index) {
    if (index == ary1.length - 1) {
        str += element;
    }else {
        str += element + "|";
    }
});
console.log(str);
```

- 将一个字符串数组的元素的顺序进行反转。["a", "b", "c", "d"] -> [ "d","c","b","a"]。使用两种种方式实现。提示：第i个和第length-i-1个进行交换

```javascript
var ary2 = ["a", "b", "c", "d"];
for (var i = 0; i < ary2.length/2; i++) {
    var temp = ary2[i];
    ary2[i] = ary2[ary2.length-1-i];
    ary2[ary2.length-1-i] = temp;
}
console.log(ary2);
console.log(ary2.reverse());
```

- 工资的数组[1500, 1200, 2000, 2100, 1800] 将工资低于2000的放到一个新数组中

```javascript
// 方式1 可用 forEach
var array =  [1500,1200,2000,2100,1800];
var tmpArray = [];
for (var i = 0; i < array.length; i++) {
  if(array[i] < 2000) {
    tmpArray.push(array[i]);
  }
}
console.log(tmpArray);
// 方式2
var array =  [1500, 1200, 2000, 2100, 1800];
array = array.filter(function (item, index) {
  if (item < 2000) {
    return true;
  }
  return false;
});
console.log(array);
```

- ["c", "a", "z", "a", "x", "a"]找到数组中每一个a出现的位置

```javascript
var ary4 = ["c", "a", "z", "a", "x", "a"];
var index = 0;
while (ary4.indexOf("a", index) != -1) {
    console.log(ary4.indexOf("a",index));
    index = ary4.indexOf("a",index) + 1;
}
```

- 编写一个方法去掉一个数组的重复元素

```javascript
var ary5 =  ['c', 'a', 'z', 'a', 'x', 'a'];
// 方法1
function unique(ary) {
    var temp = {};
    var result = [];
    for (var i = 0; i < ary5.length; i++) {
        if (!temp[ary5[i]]) {
            temp[ary5[i]] = true;
            result.push(ary5[i]);
        }
    }
    return result;
}
var result = unique(ary5);
console.log(result);

// 方法2
function unique (ary) {
    var result = [];
    for (var i = 0; i < ary.length; i++) {
        if (result.indexOf(ary[i]) == -1) {
            result.push(ary[i]);
        }
    }
    return result;
}
```

- 实现一个函数 复制字符串

```javascript
function repeatStr (str, num) {
    return new Array(num + 1).join(str);
}
var str = repeatStr ("hello", 5); // hellohellohellohellohello	
console.log(str);
// 如果数组的任一元素为 undefined 或 null，使用join方法时该元素将被视为空字符串。
```

- 对象变成数组

```javascript
var obj = {a:1,b:2,c:3};
function objectToArray(obj) {
    var result = [];
    for (var attr in obj) {
        result.push(obj[attr]);
    }
    return result;
}
var result = objectToArray(obj);
console.log(result);
```



### String - 字符串

**特性: 不可变性**

var str = '123'; str[1] = 5; console.log(str) //'123'

#### 创建字符串

```javascript
// 字面量
var str1 = "hello world";
// 构造函数方法
var str2 = new String('Hello World');

// 查看变量类型
console.log(typeof str1); // string
console.log(typeof str2); // object

// 获取字符串中字符的个数
console.log(str.length);

// 通过下标获字符串中指定位置的字符
console.log(str1[0]) // h
console.log(srr2[1]) // e
```

- JavaScript中明确规定了基本数据类型的值在内存中是不可变的，也就是说每创建一个新的字符串或者给字符串变量重新赋值，在内存中都回开辟一块新的内存空间, 闲置的字符串会被回收

```javascript
var str1 = 'Hello';
str1[0] = "A";
console.log(str1); // 'Hello'

var str2 = "hello";
str2 = "world";
```



#### 常用方法

**字符串对象的常用方法字符串所有的方法，都不会修改字符串本身(字符串是不可变的)，操作完成会返回一个新的字符串**

##### slice()

+ 返回截取后的字符串, `截取是只能从左往右截取,` 包含 start 位置的字符串, 不包含 end 位置的字符串; 
+ str.slice(start, end)
  + 无参数时, 为全部截取, 并返回
  + 只有第一个参数时, 从 start 位置截取到最后, 并返回
+ 可以使用负数, 字符串尾部索引为 -1
  + '123'.slice(-2,-1)  // 2   '123'.slice(-1)  // 3

##### substr()

+ 返回的是从 start 位置截取 length 长度后的字符串, 包含 start 位置的字符串
+ str.substr(start, length)
  + 无参数时, 为全部截取, 并返回
  + 只有第一个参数, 返回从 start 位置到末尾的字符串

##### indexOf()

+ 返回的是查找匹配到的第一个字符串的位置, 第二个为可选参数, 表示从start位置开始查找(包含start位置) ,找不到则返回-1
+ str.indexOf(str, start)
  + '1232'.indexOf('323') // -1

##### split()

+ 返回的是以分隔符切割后的字符串的数组, 第二个参数可以省略, 表示返回数组的长度, 只能使数组变短, 不能变长
+ str.split('=', length)
  + '1=2'.split('=', 3) // ['1', '2']

##### replace()

+ 替换匹配到的第一个字符串, 返回替换后新的字符串
+ str.replace("要替换的字符串"/正则表达式,"替换后的字符串"/callback)
  + 第一个参数可以为要替换的字符串, 或者一个正则表达式(如果正则表达式有全局替换符 g , 则会匹配到所有符合的字符串 )
  + 第二个参数可以为替换后的字符串, 或者一个回调函数, 回调函数的第一个参数为匹配到的字符串, 该回调函数需要一个return一个返回值来替换匹配到的字符串
    + '1232'.replace(/[2]/g, '3');  //  '1333'
    + '1232'.replace('2', '3');  // '1332'

##### search()

+ 返回匹配到的第一个字符串的位置
+ str.search(string/正则表达式)
  + 注意: 即使正则表达式有全局匹配符g, 也只会返回匹配到的第一个字符串的位置
  + '1232'.search(/[2]/g)  // 1

```javascript
// 1 字符方法
charAt(0)    	// 返回指定位置处字符, 找不到返回 空字符串''
str[0]   		// HTML5，IE8+支持 和charAt()等效 找不到返回 undefined

// 2 字符串操作方法
concat(newStr,...)   		// 拼接字符串，等效于+，+更常用
substring(strat, end) 	    // 返回的是截取后的字符串,包含开始位置的字符串,不包含结束位置的字符串 (与slice的区别主要在参数为负数上 基本用不到)

// 3 位置方法
lastIndexOf(str, start) 	// 从后往前找，返回的是查找匹配的第一个字符的索引值(为正数索引), 第二个参数可以省略, 表示从start位置开始查找(包含start位置, 从-1开始), 找不到则返回-1

// 4 去除前后的空格
trim()  		// 只能去除字符串前后的空白

// 5 大小写转换方法
toUpperCase() 	// 转换大写
toLowerCase() 	// 转换小写
toLocalUpperCase() 	// 转换大写
toLocalLowerCase() 	// 转换小写

// 6 其它
charCodeAt(索引) // 返回的是指定索引位置的字符串的Unicode码值 找不到返回NaN
String.fromCharCode(Unicode码, ...) // String.fromCharCode(101, 102, 103);	 //把Unicode码转换成字符串
```



#### ASCII码

ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）

定义了大小写字母, 阿拉伯数字, 键盘按键和特殊符号的字符编码方案, 单字节显示, 一共包含128个字符, 其中0～31及127(共33个)是控制字符或通信专用字符(其余为可显示字符), 

##### 常用ASCII码

48~57为10个阿拉伯数字, 65～90为26个大写英文字母，97～122为26个小写英文字母

37~40为键盘上的←↑→↓键

ESC键VK_ESCAPE (27)

回车键：VK_RETURN (13)

TAB键：VK_TAB (9)

Shift键：VK_SHIFT (16)

Ctrl键：VK_CONTROL (17)

Alt键：VK_MENU (18)

空格键：VK_SPACE (32)

退格键：VK_BACK (8)

鼠标右键快捷键：VK_APPS (93)

Page Up：VK_PRIOR (33)

PageDown：VK_NEXT (34)

Delete键：VK_DELETE (46)



#### Unicode码

Unicode是国际组织制定的可以容纳世界上所有文字和符号的字符编码方案。被译为万国码、统一码或单一码。

其中前一部分的ASCLL码, 没有动还是以一字节显示, 中文汉字部分采用3字节显示

Unicode可以理解成是一本很厚的字典，记录着世界上所有字符对应的数字。



#### 案例

- 截取字符串"我爱中华人民共和国"，中的"中华"

```javascript
var s = "我爱中华人民共和国";
s = s.substr(2,2);
console.log(s);
```

- "abcoefoxyozzopp"查找字符串中所有o出现的位置

```javascript
var s = 'abcoefoxyozzopp';
var array = [];
do {
  var index = s.indexOf('o', index + 1);
  if (index != -1) {
    array.push(index);
  }
} while (index > -1);
console.log(array);
```

- 把字符串中所有的o替换成!

```javascript
var s = 'abcoefoxyozzopp';
while (s.indexOf("o") != -1) {
    s = s.replace("o","!");
}
console.log(s);
```

- 判断一个字符串中出现次数最多的字符，统计这个次数

```javascript
var s = 'abcoefoxyozzopp';
var o = {};

for (var i = 0; i < s.length; i++) {
  var item = s.charAt(i);
  if (o[item]) {
    o[item] ++;
  }else{
    o[item] = 1;
  }
}

var max = 0;
var char ;
for(var key in o) {
  if (max < o[key]) {
    max = o[key];
    char = key;
  }
}

console.log(max);
console.log(char);
```

- 将字符串中问号后面的内容转换为对象格式

```javascript
var site = "http://www.baidu.com?name=zhangsan&age=20&sex=男"; // {name:"张三",age:20,sex:"男"}
var index = site.indexOf("?") + 1;
var str = site.slice(index);
var arr = str.split("&");
var result = {};
for (var i = 0; i < arr.length; i++) {
    var current = arr[i];
    var arr2 = current.split("=");
    result[arr2[0]] = arr2[1];
}
console.log(result);
```



### 基本包装类型

为了方便操作基本数据类型，JavaScript还提供了三个特殊的引用类型：String/Number/Boolean

```javascript
// 下面代码的问题？
// s1是基本类型，基本类型是没有方法的
var s1 = 'zhangsan';
var s2 = s1.substring(5); // san

// 当调用s1.substring(5)的时候，先把s1包装成String类型的临时对象，再调用substring方法，最后销毁临时对象, 相当于：
var s1 = new String('zhangsan');
var s2 = s1.substring(5);
s1 = null;
```

```javascript
// 注意点
var num = 18;  				// 数值，基本类型
var num = Number('18'); 	// 类型转换
var num = new Number(18); 	// 基本包装类型，对象
// Number和Boolean基本包装类型基本不用，使用的话可能会引起歧义。例如：
var b1 = new Boolean(false);
var b2 = b1 && true;		// true
```

```javascript
// toFixed() 方法可把数字四舍五入为指定小数位数的数字字符串。
var num = 3.4464;
var str = num.toFixed(2);
console.log(str) // "3.45"
```



### Math对象

Math对象不是构造函数，它具有数学常数和函数的属性和方法，都是以静态成员的方式提供

```javascript
Math.PI						          // 圆周率 π
Math.random()				          // 生成随机数[0, 1)
Math.floor(num)/Math.ceil(num)	      // 向下取整/向上取整
Math.round(num)				          // 取整，四舍五入
Math.abs(num)					      // 绝对值
Math.max(num1,...)/Math.min(num1...)  // 最大值/最小值

Math.sin(num)/Math.cos(num)		      // 正弦/余弦
Math.pow(num, n)/Math.sqrt(num, n)    // 指数次幂/平方根 

// 公式: 返回从x到y之间的随机数(y > x)
Math.random() * (y - x) + x           
```



### 常用字符实体

```
&yen;           ¥ 人民币符号
&nbsp;          空格
&lt;            <
&gt;            >
&reg;           ® 注册商标
&copy;          ® 防伪标识
&amp;           &
&quot;          "
```

