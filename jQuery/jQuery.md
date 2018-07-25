# jQuery(write less do more)

## 优点

```
多种选择器
链式编程: 可以用 . 符号连接的方式实现多个不同的方法的链式调用; 中途可以改变对象的指向 通过 find() siblings() parent()等
隐式迭代: $ 选择器内部有循环
丰富的插件系统
```

## 版本

```
1.xx
	兼容性最好, 支持ie6 7 8, 提供源码版和压缩版
2.xx
	不支持, ie6 7 8, 提供源码版和压缩版
3.xx
	做了大量内部优化, 提高运行速度, 不支持, ie6 7 8, 提供源码版和压缩版和精简源码版 slim (无ajax)和精简压缩版
```

## 使用方式

```
使用jQuery的三个步骤：
- 引入jQuery文件
- 入口函数
- 功能实现
```

## CDN

```
国内:
	百度  src="http://libs.baidu.com/jquery/1.10.2/jquery.min.js"
	又拍云 src="http://upcdn.b0.upaiyun.com/libs/jquery/jquery-2.0.2.min.js"
	新浪 src="http://lib.sinaapp.com/js/jquery/2.0.2/jquery-2.0.2.min.js"
```

## 多库共存

```javascript
一个文件中引入多个库时, 可能会存在 $ 符号冲突的现象;
引入库文件时将jQuery文件放在其他库文件下面引用, 否则$符不能正确释放

方法1: 
	卸载$符号  使用 新名字 代替$符号
  	var 新名字 = jQuery.noConflict();
方法2:
	由于$===jQuery, 使用jQuery代替$符号   
方法3:
	在立即调用函数中使用 $ 
	(function ($) { 继续使用$ })(jQuery);
方法4:
	转移jQuery对象到另一个对象
	var dom.jQuery = jQuery.noConflict(true);
```

## 入口函数

### window.onload

```javascript
当页面中的所有元素, 连接, 图片等全部加载完成后, 此事件触发
js创建入口函数  正常情况下只能调用一次, 第2次调用相当于重新赋值会覆盖前一个入口函数, 封装之后可调用多次
window.onload = function () {}
封装代码:
function addOnload(fn) {
  //未赋值情况下为null
  var old = window.onload;
  if (!old) {
    window.onload = fn;
  } else {
    window.onload = function () {
      old();
      fn();
    }
  }
}
```

### jQuery入口函数

```javascript
当页面的dom树生成完毕之后, 此事件触发, 可以重复调用, 不会覆盖
使用方法1:
	$(function () { 代码 }); 或者 jQuery(function () { 代码 });
使用方法2:
	$(document).ready(function(){ 代码 });  或者 jQuery(document).ready(function(){ 代码 });
```

## jQuery对象和DOM对象

### DOM对象

- 用原生JavaScript获取的DOM对象
  - 通过document.getElementById()  返回的是元素(DOM对象)


- 通过document.getElementsByTagName()获取到的是什么？
  - 伪数组(集合)，集合中的每一个对象是DOM对象

### jQuery对象

jQuery对象又可以叫做包装集(包装的DOM对象的伪数组)

- jQuery对象用$()的方式获取的对象
- length属性，获取对象内部的DOM元素个数

### jQuery对象和DOM对象的区别

- **jQuery对象不能使用DOM对象的成员，DOM对象不能使用jQuery对象的成员**

```javascript
// DOM对象
var box = document.getElementById('box');
// 错误
box.text('hello');
// 正确
box.innerText = 'hello';

// jQuery对象，jQuery对象加前缀$，用以区分DOM对象
var $box = $('#box');
// 错误
$box.innerText = 'hello';
// 正确
$box.text('hello');
```

### jQuery对象和DOM对象的相互转换

- DOM对象转换成jQuery对象

  把DOM对象转换成jQuery对象，让我们可以使用jQuery提供的众多的方法**方便操作**。

  - $(DOM对象) 


- jQuery对象转换成DOM对象 

  jQuery对象是包装集(集合)，从集合中取数据可以使用索引的方式

  - jQuery对象[索引值]
  - jQuery对象.get(索引值)

## 核心

### index()

```
$('').index(DOM对象 | jQuery对象) 
	返回 DOM对象 或者 jQuery对象 在当前选择器中的索引, jQuery对象找不到返回 -1, DOM对象找不到返回 0
	所以不建议使用 DOM对象查找
$('').index();
	不传递参数，返回这个元素在html文档中同辈中的索引位置。
```

### each()	

+ jQuery的隐式迭代会对所有的DOM对象设置相同的值，但是如果我们需要给每一个对象设置不同的值或者获取每一个对象的属性的时候，就需要自己进行迭代了。

```
jQuery伪元素集合.each(function (index, value) {
  // index 为索引
  // 此处 this 和 v 均为dom对象
})
```

### $.each()

```javascript
可以遍历数组对象和伪数组
数组遍历:
$.each(arr, function (index, item) {
  // index 为索引 item 为值
  // this 简单类型为包装类型, 复杂类型不变
});
对象遍历:
$.each(obj, function (key, value) {
  // key 为键名 value 为属性值
  // this 简单类型为包装类型, 复杂类型不变
});
```

### $.extend

+ 用一个或多个其他对象来扩展一个对象，返回被扩展的对象。

```javascript
$.extend([deep], target, obj[, obj2]);
参数: 
	deep: 可选参数 默认为false(浅拷贝), 如果为true, 则表示递归合并(深拷贝)
	target: 要拓展的对象
	obj: 待合并到第一个对象的对象
```

## 选择器

```
jQuery选择器返回的是jQuery对象。
- jQuery可以使用css的选择器来获取想要的元素
- jQuery选择器有很多，基本兼容了CSS1到CSS3所有的选择器
- jQuery还添加了很多更加复杂的选择器。
```

### jQuery基本选择器

| 名称     | 用法                | 描述                     |
| ------ | ----------------- | :--------------------- |
| ID选择器  | $('#id')          | 获取指定ID的元素              |
| 类选择器   | $('.class')       | 获取同一类class的元素          |
| 标签选择器  | $('div')          | 获取同一类标签的所有元素           |
| 并集选择器  | $('div, p, li')   | 使用逗号分隔，只要符合条件之一就可。     |
| 交集选择器  | $('div.redClass') | 获取class为redClass的div元素 |
| 通配符选择器 | $('div  *')       | 获取div的所有后代元素           |

### jQuery层级选择器

| 名称      | 用法           | 描述                              |
| ------- | ------------ | :------------------------------ |
| 直系子代选择器 | $('ul > li') | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素  |
| 后代选择器   | $('ul li')   | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等 |
| 相邻兄弟选择器 | $('li + a')  | 使用加号, 获取紧邻着li标签的a标签             |
| 兄弟选择器   | $('div ~ p') | 使用~号, 获取div 后面的所有兄弟p标签          |

### jQuery过滤(伪类)选择器

- 这类选择器都带冒号:

| 名称         | 用法            | 描述                                 |
| ---------- | ------------- | :--------------------------------- |
| :eq(index) | $('li:eq(2)') | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始。 |
| :odd       | $('li:odd')   | 获取到的li元素中，选择索引号为奇数的元素              |
| :even      | $('li:even')  | 获取到的li元素中，选择索引号为偶数的元素              |
| :gt(index) | $('li:gt(2)') | 获取到的li元素中，选择索引号大于2的元素              |
| :lt(index) | $('li:lt(2)') | 获取到的li元素中，选择索引号小于2的元素              |

### jQuery筛选选择器(方法)

- 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法。

| 名称                 | 用法                         | 描述                       |
| ------------------ | -------------------------- | :----------------------- |
| children(selector) | \$('ul').children('li')    | 相当于\$('ull > i')，直系子代选择器 |
| find(selector)     | \$('ul').find('li')        | 相当于\$('ul li'),后代选择器     |
| siblings(selector) | $('#first').siblings('li') | 查找所有兄弟节点，不包括自己本身。        |
| parent()           | $('#first').parent()       | 查找父亲                     |
| eq(index)          | $('li').eq(2)              | 选择当前选择器中索引为 2 的 li 元素    |
| next()             | $('li').next()             | 找下一个兄弟                   |
| prev()             | $('li').prev()             | 找上一个兄弟                   |
| .nextAll()         | $('li').nextAll()          | 找下面的所有兄弟                 |
| .prevAll()         | $('li').prevAll()          | 找上面的所有兄弟                 |

## 事件

### hover()

```
鼠标移入移出事件
$().hover(mouseenter, mouseleave) 两个参数, 都是函数, 第一个为鼠标移入函数, 第二个为鼠标移出函数, 无事件冒泡
```

### 常用事件

| 事件名        | 事件描述       |
| ---------- | ---------- |
| click      | 单击事件       |
| dblclick   | 双击事件       |
| mouseover  | 鼠标移入       |
| mouseout   | 鼠标移出       |
| mouseenter | 鼠标移入       |
| mouseleave | 鼠标移出       |
| mousemove  | 鼠标移动       |
| mousedown  | 鼠标按下       |
| mouseup    | 鼠标抬起       |
| keydown    | 键盘按下       |
| keypress   | 键盘按下       |
| keyup      | 键盘抬起       |
| scroll     | 滚动事件       |
| blur       | 失去焦点       |
| change     | 文本改变并且失去焦点 |
| focus      | 获得焦点时      |
| resize     | 浏览器窗口大小改变  |
|            |            |
|            |            |



## jQuery样式操作

### css操作

- 功能：设置或者获取样式，外链样式也可获取,  设置样式操作的是元素的行内 style 属性。
- 操作单个样式

```javascript
// name：需要设置的样式名称 建议全部使用字符串驼峰格式
// value：对应的样式值 除像素单位可以为数字类型 剩下样式值建议全部使用字符串驼峰格式
$obj.css(name, value);
// 使用案例
$('#one').css('background','gray');// 将背景色修改为灰色
```

- 设置多个样式

```javascript
// 参数是一个对象，对象中包含了需要设置的样式名和样式值
$obj.css(obj);
// 使用案例
$('#one').css({
    'background':'gray',
    'width':'400px',
    'height':'200px'
});
```

- 获取样式

```javascript
// name:需要获取的样式名称
$obj.css(name);
// 案例
$('div').css('backgroundColor');
```

**注意：获取样式操作只会返回第一个元素对应的样式值。**

隐式迭代：

1. 设置操作的时候，如果是多个元素，那么给所有的元素设置相同的值.
2. 获取操作的时候，如果是多个元素，那么只会返回第一个元素的值。

### class操作

- 添加样式类

```javascript
// name：需要添 加的样式类名，可以一次添加多个, 用 逗号 隔开即可, 注意参数不要带点.
$obj.addClass(name[, extra]);
// 例子,给所有的div添加one, two的样式。
$('div').addClass('one, two');
```

- 移除样式类

```javascript
// name:需要移除的样式类名, 可以一次移除多个, 用 逗号 隔开即可
$obj.removeClass(name[, extra]);
// 例子，移除div中one, two的样式类名
$('div').removeClass('one, two');
```

- 判断是否有某个样式类

```javascript
// name:用于判断的样式类名，返回值为true false
$obj.hasClass(name)
// 例子，判断第一个div是否有one的样式类
$('div').hasClass('one');
```

- 切换样式类

```javascript
// name:需要切换的样式类名，如果有，移除该样式，如果没有，添加该样式。
$obj.toggleClass(name);
// 例子
$('div').toggleClass('one');
```

## jQuery操作属性

### attr操作

```
获取或者设置元素的特性 行内属性 自定义属性
```

- 设置单个属性

```javascript
// 第一个参数：需要设置的属性名
// 第二个参数：对应的属性值
$obj.attr(name, value);
// 用法举例
$('img').attr('title','哎哟，不错哦');
$('img').attr('alt','哎哟，不错哦');
```

- 设置多个属性

```javascript
// 参数是一个对象，包含了需要设置的属性名和属性值
$obj.attr(obj)
// 用法举例
$('img').attr({
    'title':'哎哟，不错哦',
    'alt':'哎哟，不错哦',
    'style':'opacity:.5'
});
```

- 获取属性

```javascript
// 传需要获取的属性名称，返回对应的属性值
$obj.attr(name)
// 用法举例
var oTitle = $('img').attr('title');
alert(oTitle);
```

- 移除属性

```javascript
// 参数：需要移除的属性名，
$obj.removeAttr(name);
// 用法举例
$('img').removeAttr('title');
```

**案例**：美女相册

### prop操作

- 在jQuery1.6之后，对于checked、selected、disabled这类boolean类型的属性来说，不能用attr方法，只能用prop方法。

```javascript
// 设置属性
$(':checked').prop('checked', true);
// 获取属性
$(':checked').prop('checked');// 返回true或者false
```

### val()/text/()html()

```javascript
$obj.val()		获取或者设置表单元素的value属性的值
$obj.html() 	对应innerHTML
$obj.text()		对应innerText/textContent，处理了浏览器的兼容性
```

## jQuery动画

### 三组基本动画

- 显示(show)与隐藏(hide)与切换(toggle)是一组动画：
- 滑入(slideUp)与滑出(slideDown)与切换(slideToggle)，效果与卷帘门类似
- 淡入(fadeIn)与淡出(fadeOut)与切换(fadeToggle)

```javascript
$obj.show([speed], [easing], [callback]);
默认左上角进行缩放 操作 width height display:none/block属性
// speed(可选)：动画的执行时间
	 // 1.如果不传，就没有动画效果, 直接显示隐藏。如果是slide和fade系列，会默认为normal(400).
	 // 2.单位为毫秒, 比如1000, 动画在1000毫秒执行完成(推荐).
     // 3.固定字符串，slow(600)、normal(400)、fast(200)，如果传其他字符串，则默认为normal(400)。
// easing(可选): 用来指定移动效果，默认是"swing"，可用参数"linear"
// callback(可选): 执行完动画后执行的回调函数

slideDown()/slideUp()/slideToggle();同理
默认上边框进行动画, 操作 width display:none/block属性

fadeIn()/fadeOut()/fadeToggle();同理
操作 opacity display:none/block属性

特殊: fadeTo([speed], opacity, [easing], [callback])
将元素透明度搞到指定数值, opacity为必选参数 剩下同上
```

### animate

- 自定义动画

```javascript
$(selector).animate({params},[speed],[easing],[callback]);
// {params}：要执行动画的CSS属性, 为动画最终的值, 带数字（必选）
// speed：执行动画时长（可选），默认400
// easing: 执行效果，默认为swing（缓动）慢快慢  可以是linear（匀速）
// callback：动画执行完后立即执行的回调函数（可选）

特殊使用方法:
    第一个参数 属性-值对象 为 {width:"hide||show||toggle"}  滑动隐藏/显示/切换
```

### 动画队列与停止动画

- 在同一个元素上执行多个动画，那么对于这个动画来说，后面的动画会被放到动画队列中，等前面的动画执行完成了才会执行后面的动画（联想：火车进站）。
- stop

```javascript
// stop方法：停止动画效果
stop(clearQueue, jumpToEnd);
// 第一个参数：是否清除队列
// 第二个参数：是否跳转到最终效果
使用时一般直接使用 stop() 无参数
```

## jQuery节点操作

### 创建节点

```javascript
// $(htmlStr)
// htmlStr：html格式的字符串
例:
$('<span-这是一个span元素</span>');
```

### 添加节点

```javascript
父元素.fn($选择器/元素字符串)
append prepend  	在被选元素的内部的结尾/开头插入内容
before after		在被选元素之前/之后插入内容
例:	$("p").append("<b class='text'>Hello</b>");  $("p").append($('.text'))

($选择器/元素字符串).fn(父元素) 
appendTo prependTo	把内容插入被选元素的内部的结尾/开头
例: ("<b class='text'>Hello</b>").appendTo($("p"));  $('.text').appendTo($("p"))
```

### 清空节点与删除节点

- empty：清空指定节点的所有元素，自身保留(清理门户)

```javascript
$('div').empty(); // 清空div的所有内容（推荐使用，会清除子元素上绑定的内容，源码）
$('div').html('');// 使用html方法来清空元素，不推荐使用，会造成内存泄漏，子元素绑定的事件不会被清除。
```

- remove：相比于empty，自身也删除（自杀）

```javascript
$('div').remove();
```

### 克隆节点

- 作用：复制匹配的元素

```javascript
// 返回值为复制的新元素，和原来的元素没有任何关系了。即修改新元素，不会影响到原来的元素。
$(selector).clone();
// 深度复制, 包括绑定的事件
$(selector).clone(true);
```

## jQuery尺寸和位置操作

### width方法与height方法

- 设置或者获取宽度/高度(数字格式默认为单位为 px )，不包括内边距、边框和外边距
- 获取的值均数字类型
- 设置时带单位写为字符串格式

```javascript
// 带参数表示设置高度
$('img').height(200);
// 不带参数获取高度
$('img').height();
```

获取网页的可视区宽高

```javascript
// 获取可视区宽度
$(window).width();
// 获取可视区高度
$(window).height();
```

### innerWidth/innerHeight/outerWidth/outerHeight

```javascript
全部为只读属性, 获取的值均为数字类型
innerWidth()/innerHeight()	方法返回元素的宽度/高度（包括内边距）。
outerWidth()/outerHeight()  方法返回元素的宽度/高度（包括内边距和边框）。
outerWidth(true)/outerHeight(true)  方法返回元素的宽度/高度（包括内边距、边框和外边距）。
```

### scrollTop与scrollLeft

- 设置或者获取元素卷曲出去的距离
- 获取时均为数字类型
- 默认为数字类型单位为 px 

```javascript
// 获取页面被卷曲的高度
$(window).scrollTop();
// 获取页面被卷曲的宽度
$(window).scrollLeft();

设置页面卷曲的高度时使用 $('html, body').scrollTop(值)
```

### offset方法与position方法

- offset方法获取元素距离document(页面)左上角的位置
- position方法获取的是元素相对于距离最近的且定位不为static的父元素(offsetParent)的位置。
- 返回的值都为对象
- offset可设置 position不可设置

```javascript
// 获取元素距离document的位置,返回值为对象：{left:100, top:100} 相对于浏览器可视区域左上角的距离
$(selector).offset();
// 获取相对于其最近的有定位的父元素的位置。子元素的margin左上角相对于父元素的padding的左上角
$(selector).position();
```

## jQuery事件机制

- JavaScript中已经学习过了事件，jQuery对JavaScript事件进行了封装，增加并扩展了事件处理机制。jQuery不仅提供了更加优雅的事件处理语法，而且极大的增强了事件的处理能力。

### jQuery事件发展历程(了解)

简单事件绑定--bind事件绑定--delegate事件绑定--on事件绑定(推荐)

- 简单事件注册

```javascript
click(handler)			单击事件
mouseenter(handler)		鼠标进入事件
mouseleave(handler)		鼠标离开事件
```

缺点：不能同时注册多个事件

- bind方式注册事件

```javascript
// 第一个参数：事件类型
// 第二个参数：事件处理程序
$('p').bind('click mouseenter', function(){
    // 事件响应方法
});
```

缺点：不支持动态事件绑定

- delegate注册委托事件

```javascript
// 第一个参数：selector，要绑定事件的元素
// 第二个参数：事件类型
// 第三个参数：事件处理函数
$('.parentBox').delegate('p', 'click', function(){
    // 为 .parentBox下面的所有的p标签绑定事件
});
```

缺点：只能注册委托事件，因此注册时间需要记得方法太多了

- on注册事件

### on注册事件(重点)

- jQuery1.7之后，jQuery用on统一了所有事件的处理方法。
- 最现代的方式，兼容zepto(移动端类似jQuery的一个库)，强烈建议使用。

on注册简单事件

```javascript
// 表示给$(selector)绑定事件，并且由自己触发，不支持动态绑定。
$(selector).on( 'click', function() {});
```

on注册事件委托

```javascript
// 表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定
$(selector).on( 'click','span', function() {});
```

事件委托原理

```javascript
// 事件委托的原理
var ul = document.querySelector('#ul');
ul.onclick = function (e) {
  // console.log(e.target.tagName);
  if (e.target.tagName.toLowerCase() === 'li') {
    // 可执行函数
    fn();
  }
}
```

on注册事件的语法：

```javascript
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
// 第四个参数：handler，事件处理函数
$(selector).on(events[,selector][,data],handler);
```

- click bind delegate on 注册事件的区别
- click 由 js 原生事件封装
- bind delegate由 jQuery  on注册事件封装 

### 事件解绑

- unbind方式（了解 不用）

```javascript
$(selector).unbind(); // 解绑所有的事件
$(selector).unbind('click'); // 解绑指定的事件
```

- undelegate方式（了解 不用）

```javascript
$( selector ).undelegate(); // 解绑所有的delegate事件
$( selector).undelegate( 'click' ); // 解绑所有的click事件
```

- off方式（推荐）

```javascript
// 解绑匹配元素的所有事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off('click');
```

### one注册事件

+ 为每一个匹配元素的特定事件（像click）绑定一个一次性的事件处理函数。

```
$().one(type,[data],fn) 
参数: type 事件类型  data 可选参数 传递的数据  fn 可执行函数
例: 
$("p").one("click", function(){
  alert( $(this).text() );
});
```

### 触发事件

```javascript
$(selector).click(); // 触发 click事件 前提已经绑定事件
$(selector).trigger('click');
```

### jQuery事件对象

jQuery事件对象其实就是js事件对象的一个封装，处理了兼容性。

```javascript
以下属性都在元素可见区域有效 除 margin 的部分 
// screenX和screenY	  距离电脑屏幕最左上角的值
// clientX和clientY	  距离浏览器可视区域左上角的位置（忽视滚动条）
// pageX和pageY	      距离页面(document)最顶部的左上角的位置（会计算滚动条的距离）
offset存在问题, 父元素注册事件在子元素触发时,获取的是子元素的内部坐标
// offsetX和offsetY  距离当前元素padding左上角的距离 点击border会获取相应的 负值

// event.eventPhase  事件发生在哪个阶段
// event.type        事件的类型
// event.keyCode	 按下的键盘代码
// event.data	     存储绑定事件时传递的附加数据(on事件绑定时第3个可选参数)
例: $('div').on('click', data, function (e) {e.data})

// event.currentTarget   当前触发事件的元素
// event.delegateTarget  事件委托的祖先元素
// event.target          拿 click 举例 就是鼠标点谁 target 就是谁

// event.stopPropagation()	阻止事件冒泡行为
// event.preventDefault()	阻止浏览器默认行为
// return false:既能阻止事件冒泡，又能阻止浏览器默认行为。
```

## 链式编程

- 通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作(查找方法除外)的时候，会返回获取到的相应的值，无法返回 jQuery对象。

```javascript
end(); // 返回上一次操作的jQuery对象
例: $('ul li').eq(0).next().end()  // 返回$('ul li').eq(0)
```