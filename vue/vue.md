### 主流前端 JavaScript 框架

- Angular
  - 09年 原来是个人开发的，后来被 Google 给收购了
- React
  - 诞生于 Facebook 公司内部
- Vue.js
  - 尤雨溪（中国江苏无锡人，12 年左右）
  - 屌丝福音，中文文档非常友好

目前在公司中，BAT 级别的企业：React  -》 Angular -》 Vue.js 多一些。

在中小型公司，Vue.js 更多一些。

### Vue.js 介绍

- 是什么
  - 前端 JavaScript 框架
- 为什么用它
  - 它能帮助提升网站应用程序开发效率
- 一般什么情况下使用它
  - 一般是需要开发 SPA 应用程序的时候去用
  - 但是 Vue 是渐进式的，Vue 其实可以融入到不同的项目中
    - 可以和传统的网站开发架构融合在一起，例如可以简单的把它当作一个类似 jQUery 的库来使用
    - 也可以使用它开发大型的 SPA 单页面应用程序
- 发展历史
  - 作者：尤雨溪（微博：尤小右），设计出身。tj 也是设计出身。
    - [个人网站](http://evanyou.me/)
    - [知乎](https://www.zhihu.com/people/evanyou/activities)
    - [新浪微博](http://weibo.com/arttechdesign)
  - 作者尤雨溪最初在 2013 年 12 月 8号在 GitHub 上发布了 0.6 版
  - 2015 年 10 月份正式发布了 1.0 版本
    - Vue 真正的火起来就是在 15 年的 1.0 版发布之后才简陋头角
  - 2016 年 10 月份正式发布了 2.0 版
  - 截止到 2017-11-9 16:24:15 最新版是 2.5.3
  - 作为学习者，学习最新版即可
  - 1.0 老的项目可能还在用，新项目绝对都是选择 2.0

### 安装

- Vue.js 不支持 IE8 及其以下版本，因为 Vue.js 使用了 IE8 不能模拟的 ECMAScript 5 特性。Vue.js 支持所有[兼容 ECMAScript 5 的浏览器](http://caniuse.com/#feat=es5)。
- 发布日志：https://github.com/vuejs/vue/releases
- 直接下载
- npm
  - `npm install vue`
  - 简写 `npm i vue`

### Vue 实例

- el
  - 指定被 Vue 管理的模板入口，网页中的 DOM 节点
  - 不能使用 body、html
  - 必须是一个普通的 HTML 标签节点，一般是 div
- 虚拟标签 template
  - 一般与 v-if 配合使用;隐藏多标签区域
  - 没有具体的实体;不产生新的标签;在网页中不显示; 解析后的文档中也不存在
- data
  - 作用：**数据驱动视图** 中的 **数据**
  - 不是什么数据都往里面初始化的
  - 一般都是根据你的视图来初始化需要使用：数据驱动视图功能的数据
  - 现在就是不需要 id 了，只需要在 data 中初始化一个数据成员，然后在模板中绑定使用这个成员
    - 则我们就可以通过修改数据的方式来改变视图
  - 核心就是把 DOM 操作的思想转变到 **数据驱动视图** 的思想
- methods
  - 作用：一般用来定义事件处理函数
  - 虽然我们可以把方法写到 data 中，但是在 Vue 中更推荐把所有方法都写到 methods 属性中
  - 这样做更合理，数据和方法分开，分门别类
  - 不允许具有和 data 中重名的成员,否则会报错

```javascript
new Vue({
  el:
  data:
  methods:
})
```



### 数据绑定渲染(指令)

- v-text

  - 更新元素的 `textContent`。如果要更新部分的 `textContent` ，需要使用 `{{ Mustache }}` 插值。
  - 使用时  <span v-text="msg"></span>  无闪烁现象

- v-html

  - 更新元素的 `innerHTML` 。**注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译**。
  - 不会渲染html字符串中带有script标签的字符串 防止xss(跨域网站攻击)
  - 在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 [XSS 攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。只在可信内容上使用 `v-html`，**永不**用在用户提交的内容上。

- v-show

  - 根据表达式之真假值，切换元素的 `display` CSS 属性。当条件变化时该指令触发过渡效果。

  - ```
    <span v-show='表达式'></span>
    ```

- v-if

  - 根据表达式的值的真假条件渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建。

  - 在文档中显示为 为false时如果已经存在该元素则删除该元素,如果没有不做处理 为true时 动态添加该元素

  - 如果元素是 `<template>` ，将提出它的内容作为条件块。当条件变化时该指令触发过渡效果。

  - ```
    <span v-if='表达式'></span>
    ```

- v-else-if     注意 : 为2.1版本新增元素

  - 前一兄弟元素必须有 `v-if` 或 `v-else-if`。

  - ```
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
    ```

- v-else

  - 前一兄弟元素必须有 `v-if` 或 `v-else-if`。

  - ```
    <div v-if="Math.random() > 0.5">
      Now you see me
    </div>
    <div v-else>
      Now you don't
    </div>
    ```

- 文本绑定： `{{}}`

  - mustache(八字胡) 语法 使用时   {{ msg }}
  - 有一些问题 在加载渲染时 会有闪烁现象
  - 解决办法为 使用v-cloak指令

- v-cloak

  - 在数据完全渲染完成前使元素处于隐藏状态 知道渲染完成显示元素

  - ```
    css代码  建议直接内嵌在主文档中
    [v-cloak] {
      display: none;
    }
    直接在想要实现的元素上添加v-cloak指令即可
    <div v-cloak>
      {{ message }}
    </div>
    ```

- 属性绑定： `v-bind`
  - 在标签节点的属性中绑定使用 data 中数据成员，则必须使用 v-bind 指令来处理
  - 简写：`:属性名称="表达式"` 表达式可以为 简单表达式,   vue 数据, 字符串 或者是对象 数组

- 动态切换绑定属性
  - :class='{clearFix:flag}' 当 flag 为 true时应用此属性 反之相反
  - 也可以为 boolean 之外的类型 vue会默认强制转换其类型  例如 : data.length

- 这里是数据变，视图变  单项数据绑定
  - 视图变，数据不会变

数据绑定：

```html
<!-- data 中的成员 message -->
<h1>{{ message }}</h1>

<!-- 字符串 message -->
<h1>{{ 'message' }}</h1>

<!-- 数字 123 -->
<p>{{ 123 }}</p>

<!-- 错误的用法 -->
<h1 foo="{{ message }}">测试文本</h1>

<!-- 绑定 data 中的成员 message，正确的用法，也是响应式的 -->
<h1 v-bind:foo="message">测试文本</h1>

<!-- 字符串 message -->
<h1 v-bind:foo="'message'">测试文本</h1>
```

使用 JavaScript 表达式：

```javascript
可进行一些计算的简单操作
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
```

+ v-pre
  + 跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache( {{ }} ) 标签。跳过大量没有指令的节点会加快编译。一般用在大篇幅不需要编译的文章上.
  + <span v-pre>{{ this will not be compiled }}</span>
  + <blockquote v-pre>引用的文章</blockquote>
+ v-once
  + 只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。
  + <span v-once>This will never change: {{msg}}</span>

### class与style绑定

```
在将 v-bind 用于 class 和 style 时，Vue.js 做了专门的增强。表达式结果的类型除了字符串之外，还可以是对象或数组。

注意 : CSS 属性名可以用驼峰式(推荐使用) (camelCase) 或短横线分隔 (kebab-case，记得用单引号括起来) 

对象语法
v-bind:class 指令也可以与普通的 class 属性共存。当有如下模板:
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
和如下 data：
data: {
  isActive: true,
  hasError: false
}
结果渲染为：
<div class="static active"></div>

数组语法
我们可以把一个数组传给 v-bind:class，以应用一个 class 列表：
<div v-bind:class="[activeClass, errorClass]"></div>
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
渲染为：
<div class="active text-danger"></div>
如果你也想根据条件切换列表中的 class，可以用三元表达式：
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```



### 表单数据双向绑定

- 双向数据绑定  v-model='数据'
  - 数据的变化会引起绑定该数据的视图的变化
  - 视图的变化会引起绑定改视图的数据的变化
  - 在多选按钮中使用 v-model 绑定数据值为 布尔类型时 会将此值应用到checked属性上,也就是说会控制多选框的选择状态


- 文本
- 多行文本
- 复选框
- 单选按钮
- 选择列表

### 事件处理

+ 事件处理函数中的 this 为vue实例对象

- 定义事件处理函数

  - 在vue属性methods中定义事件处理函数
  - 可使用简写    fn () {}

- 绑定事件处理函数
  - `v-on:事件名称="事件处理函数"`

  - 缩写：`@事件名称="事件处理函数"`

  - 事件处理函数可以传参数 传其他参数并且还想要使用事件参数对象,就在最后传一个  `$`event ,在事件处理函数中就可使用 event 对象 例 : @click='fn(item,$event)'

  - **修饰符**： 使用时直接在 事件 后面点即可  例  @click.stop='fn'

    - `.stop` - 调用 `event.stopPropagation()`。
    - `.prevent` - 调用 `event.preventDefault()`。
    - `.capture` - 添加事件侦听器时使用 capture 模式。
    - `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
    - `.{keyCode | keyName}` - 只当事件是从特定键触发时才触发回调。
    - `.native` - 监听组件根元素的原生事件。
    - `.once` - 只触发一次回调。
    - `.left` - (2.2.0) 只当点击鼠标左键时触发。
    - `.right` - (2.2.0) 只当点击鼠标右键时触发。
    - `.middle` - (2.2.0) 只当点击鼠标中键时触发。
    - `.passive` - (2.3.0) 以 `{ passive: true }` 模式添加侦听器

  - ```
    <!-- 方法处理器 -->
    <button v-on:click="doThis"></button>

    <!-- 对象语法 (2.4.0+) -->
    <button v-on="{ mousedown: doThis, mouseup: doThat }"></button>

    <!-- 内联语句 -->
    当 函数体 语句较少时 可以直接书写
    <button @click="return false"></button>

    <!-- 传递参数 -->
    <button v-on:click="doThat('hello', $event)"></button>

    <!-- 缩写 -->
    <button @click="doThis"></button>

    <!-- 停止冒泡 -->
    <button @click.stop="doThis"></button>

    <!-- 阻止默认行为 -->
    <button @click.prevent="doThis"></button>

    <!-- 阻止默认行为，没有表达式 -->
    <form @submit.prevent></form>

    <!--  串联修饰符 -->
    <button @click.stop.prevent="doThis"></button>

    <!-- 键修饰符，键别名 -->
    <input @keyup.enter="onEnter">

    <!-- 键修饰符，键代码 -->
    <input @keyup.13="onEnter">

    <!-- 点击回调只会触发一次 -->
    <button v-on:click.once="doThis"></button>
    ```

- 键盘事件
  - keydown || keyup || keypress
  - vue为键盘事件提供了快捷指定键绑定
  - @事件.keyCode='事件名'
  - 官方为特殊的键提供了名字
    - .enter  回车键  keyCode为13
    - .tab   tab制表键
    - .delete  删除 和 退格
    - .esc   撤销
    - .space   空格
    - .up   上
    - .down   下
    - .left   左
    - .right   右

### 条件渲染与列表循环渲染

- `v-if=''`

  - 当单独应用在标签上时;并且值为布尔类型就会控制该元素的显示/隐藏属性 (会把标签从文档中删除)
  - 与 if 一样存在隐式转换 转换规则与 if 相同 如 0 会转变为 false

- `v-for='变量 of/in 数据'`  

  - 可以遍历数组 或者 对象

  - vue推荐使用 of 循环遍历数据

  - 遍历数据并输出相应次数的 html 标签

  - ```javascript
    //遍历数组时
    <ul>
      //item 为单个数据   index 为当前数据的索引值
      <li v-for='(item, index) of data'>{{ item.name }}</li>
    </ul>
    //遍历对象时
    <div v-for="(val, key) in object"></div>
      //val为值; key为键; index为索引
    <div v-for="(val, key, index) in object"></div>
    ```

- 一起使用实现条件过滤

  - ```
     <ul>
          <!-- 
            点击三个 a 链接的时候，改变这里的 v-if 的条件
            true
            item.completed === true
            item.completed === false
           -->
          <li v-for="item in todos" v-if="true">{{ item.title }}</li>
        </ul>
      <script src="node_modules/vue/dist/vue.js"></script>
      <script>
        var app = new Vue({
          el: '#app',
          data: {
            todos: [
              {
                id: 1,
                title: 'a',
                completed: true
              },
              {
                id: 2,
                title: 'b',
                completed: false
              },
              {
                id: 3,
                title: 'c',
                completed: true
              }
            ]
          }
        })
      </script>
     ```
    ```

    ​
    ```

### Object.defineProperty

```
vue计算属性的原理
var user = {
foo: 'bar'
}

// 这个 API 一般用于框架设计
Object.defineProperty(user, 'gender', {
// value: 0,  设置属性的默认值
// value 和 get 两者只能取其一，因为是矛盾的

// 对象属性的 get 访问器
// get 方法，被用于属性访问
// 当你访问 gender 属性的时候，会自动调用 get 方法
get: function () {
console.log('gender 的 get 方法被调用了')
return 123
},

// 属性 set 设置器
// 当试图去更改该属性时 user.gender = xxx 的时候，则会自动调用 set 方法，xxx 将作为 set 方法的参数
// 参数 value 为设置后的属性值
set: function (value) {
console.log(value)
}
})
```



### 计算属性

```
- 一种特殊的属性，本质是方法，但是只能当做属性来使用
- 原理为 : EcmaScript 5：Object.defineProperty
- 计算属性不能当作方法来使用，不能调用
- 计算属性依赖数据进行缓存
- 和方法相比，推荐使用计算属性

new Vue({
  el:'',
  computed: {
    计算属性名 () {
      return 函数体
    } 
  }
})
计算属性自动 watch 了内部依赖的响应式成员
当它依赖的响应式成员发生变化，则它自己也重新计算调用

与侦听属性不同的是 : 计算属性一般为返回一个值  侦听属性一般为进行相关的一些操作
```



### 侦听属性

```
watch  为vue的一个对象属性  用于监测 data 属性中的值的变化 并作出相应的响应
watch: {
    data属性值: function (val,oldVal) {  //前一个参数为改变之后的的值,后一个参数为改变之前的值
      函数体//  一般根据数据的变化进行一些相关操作  不返回数据
    }
  }
例:     常用于永久性存储(监听数据的变化动态添加到本地或者数据库中)
<div id="demo">{{ fullName }}</div>
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    }
  }
})
```



### 组件

```
全局注册

要注册一个全局组件，可以使用 Vue.component(tagName, options)。例如：
Vue.component('my-component', {
  // 选项
})
自定义标签的命名(一定不要重复;避免使用带有原生标签的名字) : 建议遵循 W3C 规则 小写，并且包含一个短杠

组件在注册之后，便可以作为自定义元素 <my-component></my-component> 在一个实例的模板中使用。
<div id="example">
  <my-component></my-component> //此处相当于一个坑,将template属性中的字符串在此解析
</div>
注意确保在初始化根实例之前注册组件：
// 注册组件
Vue.component('my-component', {
  template: `<div>A custom component!</div>`//建议使用多行字符串
})
// 创建根实例
new Vue({
  el: '#example'
})
渲染为：
<div id="example">
  <div>A custom component!</div>
</div>

局部注册

你不必把每个组件都注册到全局。你可以通过某个 Vue 实例/组件的实例选项 components 注册仅在其作用域(单独文件)中可用的组件：
var Child = {
  template: '<div>A custom component!</div>'
}
new Vue({
  // ...
  components: {
    // <my-component> 将只在父组件模板中可用
    'my-component': Child
  }
})

data 必须是函数

构造 Vue 实例时传入的各种选项大多数都可以在组件里使用。只有一个例外：data(组件模板数据) 必须是函数。
Vue.component('my-component', {
  template: '<span>{{ message }}</span>',
  data () {
    return {
      message: 'hello'
    }
  }
})
```

