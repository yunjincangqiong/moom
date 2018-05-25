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

##requestAnimationFrame