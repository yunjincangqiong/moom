## 技巧

1. 数组数据存储 arr(arr.length) = num;    作为参考 官方建议 使用 arr.push()
2. 数组名.toString();   一般使用在历史记录的本地存储中 将数组转换为逗号分隔的字符串
3. 函数传入的参数不固定时使用 arguments 伪数组
4. ~~ 小数舍弃小数点后部分取整 与正负无关
5. 伪数组转化为数组 [].slice.call( 伪数组 )  返回值为数组
6. 判断类型 Object.prototype.toString.call( 要判断的值 )  //例 返回值为 "[Object Array]"
7. 用三元表达式替换 if-else 判断语句
8. 赋值或计算时 有些场景使用 || 或者 &&  可以更高效; 使用时注意判断截断问题
9. '1,2,3,4'.split('') 创建一个数组
10. 中文输入法全角一个空格和一个普通字一样大, 可以解决表单对齐问题
11. 数组去重 es6写法 [... new Set ( [ 1,2,3,3,3,3,1,2 ] ) ]  // [1,2,3]
12. ​



## 小知识点

1. switch-case 中匹配值的时候是按照严格的模式进行匹配的(相当于使用的是===的方式);
2. return 语句后面的代码不执行;   技巧使用在 if 语句中 有时可以不使用else
3. 函数只在当前函数所在的及其后面的 script 标签域中生效;相同的函数名会覆盖上一个函数;
4. typeof 输出任何一个未定义的变量都为 undefined;
5. 函数和变量的声明会提前,函数在变量之前,但是赋值或者是调用是不会提前;
6. 变量提升只对var命令声明的变量有效，如果一个变量不是用var命令声明的，就不会发生变量提升;(隐式变量)
7. JavaScript语言的标识符(变量,函数名)对大小写敏感;
8. 字符串可以使用string[索引]的方式获取指定位置的字符
9. table中选择 tr 不可以使用直接子元素选择器 table > tr 的方式, 因为tr还有隐藏的父元素(thead tbody tfoot)
10. position定位默认偏移值不一定是0,0  所以一定要提供left和top默认值
11. 一个完整的url地址 : 协议://域名:端口号/文件路径?参数1&参数2#锚点 
12. ​



## 布局方面

```
float 会使元素变为 blcok 元素
float 会脱离文档流 但是还会影响 文字 布局(文字环绕问题)
使用float 时 一定注意清除浮动问题(父元素塌陷问题)
float 可以 和 position 一起使用 不会相互影响
行内元素设置 宽 高 垂直外边距 不起作用 大小由内容决定
行内元素设置 垂直内边距时 元素可能会溢出
position:relative 会保留原来的位置 不会改变元素的display
position:absolute/fixed 脱离文档流 使元素变为 block 元素
使用img时注意将元素变为block元素 会解决底部白边问题
inline-block 会渲染元素标签之间的空白节点 解决办法为 取消标签之间的空白,设置字体大小为0,利用注释等
默认情况下，block元素宽度自动填满其父元素宽度
数组的遍历系列的方法 如 some every map find fingIndex forEach filter 里面的 this 默认(在不改变 this 指向的情况下,改变指向 只能用bind ;使用apply, call会自动调用回调函数是指向变为undefined)指向 window
```



## 在switch语句中使用范围值

```js
function name(num) {
  let test;
  // 将switch后面括号里面的值设置为 true, case中就可以使用范围表达式了
  switch (true) {
    case num == 0:
      test = 1
      break
      case num > 0 || num < 6:
      test = 2
      break
      default:
      test = 3
  }
  console.log(test)
}
```



## 使用对象结构赋值来获取数组中想要的值

```js
const arr = 'a,b,c,d'
// 将想获取的数组中的值得索引写到对象中, 起一个别名即可获取
const {0: v1, 3: v2} = arr.split(',')
```



## 创建一个 pure Object(纯净的对象)

pure Object: 它不继承对象的任何方法, 也就是说它身上没有挂载任何属性和方法

```js
const pureObject = Object.create(null)
console.log(pureObject.toString) // undefined
```



## 使用对象解构来模拟函数的可选配置项(命名参数)

```js
// 此处使用双重函数默认值写法
// 1. 如果没有传参数默认就为空对象
// 2. 如果对象没有传 name 和 age 属性就为默认值
function fn({name = 'gt', age = '12'} = {}) {
  console.log(name)
  console.log(age)
}
```



## 将多维数组整合成单个数组

```js
function flattenArray(arr) {
  const flattenArr = [].concat(...arr)
  return flattenArr.some(v => Array.isArray(v)) ? flattenArray(flattenArr) : flattenArr
}
```





## 强制get请求不使用缓存

```
使用 get 方法发送请求但是不使用缓存: 可以在 url 后面拼接一个不重复键值对, 例如 Math.random() 或者 Date.now(); 
原理: 浏览器从缓存加载会根据 url 查找, 从这点下手, 使每次 url 都不一样就不会从缓存加载
eg: xhr.open("GET", "/student?r=" + Math.random());
```

## 阻止form的submit事件

```
表单元素 form 的 submit 事件不可以使用 return false; 阻止, 只可以使用 e.preventDefault(); 阻止
```

```html
<!-- 可以使用伪协议阻止, 令其执行一个空的js代码 -->
<form action="javascript:;">...</form>
```

## ie条件注释

快捷键:  cc:ie + tab

```html
<!--[if lt IE 9]> 
  这里面的内容只有相应版本的ie会识别, 其余浏览器把其当成普通注释处理
<![endif]-->
<!-- lt 小于 gt 大于 lte 小于等于 gte 大于等于 -->
```

## 行内元素嵌套img标签产生的bug

```
    行内元素不设置宽高属性完全由图片元素撑起, 此时图片元素的高度不会撑起父行内元素的高度, 父元素的实际高度与字体大小有关, 为字体大小加上基线以下的高度.
    但即使如此仍然不会影响绑定在父行内元素上的事件的触发, 事件触发的范围为图片的大小范围, 也就是说触发事件时相当于行内元素被图片撑起了 
    解决方法: 将行内元素设置为不为行内元素即可 一般设置为块级元素 block, 并去除图片的下白边问题 vertical-align 属性不为 bottom 即可
```

## new Date()时间格式化

```
new Date(年(4位), 月(从0开始), 日, 时, 分, 秒).getTime(); 返回设置时间的时间戳(ms)
eg:
  new Date(2018, 4, 20, 21, 23, 25).getTime();  返回2018年5月20日21点23分25秒的时间戳
```

## 封装函数的参数问题

```html
关于封装插件(函数), 提供的参数可选时, 在函数内部创建一个相同的提供默认值的参数,并在调用函数时将使用者传入的参数覆盖内部参数 
eg:
<script>
  function swiper(myNode, options) {
    // 将所有方法和参数都提供一个默认值, 在用户不传相应的值时不会报错
    var myDefault = {
      flag: true,
      swiperLeft: function () {},
      swiperRight: function () {}
    }
    // 用使用者传的值覆盖内部默认参数
    for (let key in options) {
      myDefault[key] = options[key];
    }
  }
</script>
```

## 字体图标的使用技巧

```html
<style>	
/* 先使用 @font-face 自定义字体图标 */
@font-face {
    font-family: 'diy';
    src: url('../fonts/MiFie-Web-Font.eot') format('embedded-opentype'), 
         url('../fonts/MiFie-Web-Font.svg') format('svg'), 
         url('../fonts/MiFie-Web-Font.ttf') format('truetype'), 
         url('../fonts/MiFie-Web-Font.woff') format('woff');
}
/* 定义使用该自定义字体图标的类 */
.diy_icon {
    font-family: 'diy';
}
/* 定义使用某个字体图标的类 */
.diy_icon_phone::before {
    content: "\e908";
}

.diy_icon_tel::before {
    content: "\e909";
}
</style>
使用时添加 span标签 或者 i标签, 并添加相应的类名即可
好处: 令其水平垂直居中很简单, 为父元素添加 text-align: center, 和 height, line-height 或者给子元素添加vertical-align: middle;即可
eg: <i class="diy_icon .diy_icon_phone"></i>
```



## 协商缓存和强缓存



## 活动对象 与 变量对象

[参考链接](https://www.zhihu.com/question/36393048)

```
函数内部都有一个叫做执行环境用于控制变量和函数的访问，函数内部所有的变量和函数都保存在一个叫做变量对象中（这部分是隐式的, js中访问不到），变量对象被调用的时候就称之为活动对象，变量对象里面如果还有（函数）变量对象他们之间需要访问的这个时候又被称之为作用域链！一层层到全局执行环境！
```



## 单线程与异步与js事件机制

[参考链接](http://www.cnblogs.com/woodyblog/p/6061671.html)



## 实现.5px的细线

### 渐变

将1px高的伪元素的背景一半有颜色一半透明即可

```css
height: 1px;
background: linear-gradient(#000 50%, transparent 50%);
```

### 缩放

实现上有些问题: mac(n屏)上显示为颜色变浅了一半, 高度没有变化

```css
/* 1 */
height: 1px;
background-color: #000;
/* 2 */
border-top: 1px solid #000;

transform: scaleY(.5)
```



## webstorm快捷键

```
Alt + j                        选中下一个同样的词
Ctrl + y                       删除当前行并将光标处于原位置不动
Ctrl + Alt + L                 格式化代码
ctrl + Shift + N               通过文件名快速查找工程内的文件（必记）
ctrl + Shift + alt + N         通过一个字符快速查找位置（必记）
Shift + Ctrl + up/down         上下移动当前行
Ctrl + f                       查找
Ctrl + d                       克隆当前行
Ctrl + r                       替换
shift + f6                     重命名
Ctrl + 鼠标左键单击             快速打开光标处的类或方法
Ctrl + c                       复制
Ctrl + v                       粘贴
Ctrl + x                       剪切
Ctrl + a                       全选
Shift + Enter                  生成一个新行并把光标移动到新行开始处
Ctrl + / 或 Ctrl + Shift + /   快速注释（// 或者/*…*/ ）
Shift + Ctrl + Alt + j         选中所有同样的词
Ctrl + Shift + F7              高亮显示选中文本，按Esc高亮消失。
```

### 

