# Vue.js - day7


## 插槽

定义：定义子组件的时候，在子组件内部刨了一个坑，父组件可以往坑里填内容；

### 单个(普通, 默认)插槽

1. 定义插槽：在子组件的定义中，可以使用 `<slot></slot>` 定义一个插槽(只能定义一个)；
2. 使用插槽：在父作用域中使用带有插槽的组件时，子组件元素内容区域中的内容，会插入到插槽中显示；



### 多个（具名）插槽

1. 定义具名插槽：使用 `name` 属性为 `slot` 插槽定义具体名称；
   + eg: `<slot name="header"></slot>`
2. 使用具名插槽：在父作用域中使用带有命名插槽的组件时，需要为内容添加属性 `slot="插槽name"` 来填充到指定名称的插槽；


### 作用域插槽(比较重要)

**注意：同一组件中不同插槽的作用域，是独立的！**

1. 定义作用域插槽：在子组件中，使用 `slot` 定义插槽的时候，可以通过 `属性传值` 的形式，为插槽传递数据，普通属性和自定义属性可以正常书写, 如果要绑定 data 中的数据, 需要使用属性绑定方式    

   eg：`<slot title="game" text="hello" :msg="sonMsg"></slot>`

2. 使用作用域插槽：在父作用域中，在子组件元素中`要插入插槽的元素`通过定义 `slot-scope="scope"` 属性(属性值为合法名即可)，接收并使用 插槽数据；

   插槽数据可以通过 slot-scope 属性的属性值获取到, 其值为一个对象, 包含对应的插槽上定义的除 name 属性之外所有的属性键值对


```html
<!-- 带插槽的子组件 -->
<template>
  <div>
    <slot title="game" data-text="hello" :msg="msg"></slot>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        msg: {
          no: '0',
          txt: 'test'
        }
      }
    }
  }
</script>
<!-- 父组件 -->
<template>
  <div>
	<my-son>
      <p slot-scope="scope">{{scope}}</p> <!-- 其值为 { "title": "game", "text": "hello", "msg": { "no": "0", "txt": "test" } } -->
    </my-son>
  </div>
</template>
```

**注意: 同一作用域插槽, 只能插入一个根节点, 如果有多个后面的会把前面的覆盖**

```html
<!-- 父组件 -->
<template>
  <div>
	<my-son>
      <!-- 第二个p元素会渲染到也页面上, 第一个p元素会被覆盖 -->
      <p slot-scope="scope">111</p>
      <p slot-scope="scope">222</p>
    </my-son>
  </div>
</template>
```



## `webpack` 中配置 `省略文件后缀名` 和 `@` 路径标识符

1. 省略文件扩展名：

   `import`和`module.export`导入文件, 如果文件夹中只包含 index.js 文件可以省略文件名

   ```js
   import './router'
   ```

   + 打开 `webpack.config.js`，在导入的配置对象中，新增 resolve 属性；

   + 在 resolve 节点中，新增 `extensions` 节点：

     ```js
     resolve: {
       // resolve 节点下的 extensions 数组中，可以配置，哪些扩展名可以被省略
       // 在文件没写后缀名时, webpack会依次查找是否有匹配的后缀名的文件
       extensions: ['.js', '.vue', '.json']
     }
     ```

   + 修改完配置以后，重新运行 `npm run dev` 查看效果；

2. 配置 `@` 指向 `src` 目录：

   ```js
   resolve: {
     alias: {
       '@': path.join(__dirname, './src') // 让 @ 符号，指向了 项目根目录中的 src 目录
     }
   }
   ```




## `.vue` 组件中的样式作用域问题

1. 通过为`style`标签提供`scoped`属性, 从而让 当前组件中的样式，只在当前组件范围内生效
   + 默认，在组件中写的样式，都是全局生效的
2. 原理：通过 第一无二的属性选择器实现每个组件的 样式作用域；




## 在项目中安装和使用`element-ui`

[element-ui 官网](http://element-cn.eleme.io/#/zh-CN)

element-ui 是 饿了么 前端团队，开源出来的一套 Vue 组件库；

使用方法与 bootstrap 相同, 查文档 - 复制 - 粘贴 - 修改

**完整引入 `Element-UI` 组件：**

1. 运行 `npm i element-ui` 安装组件库

2. 在 `index.js` 中，导入 `element-ui` 的包、配套样式表、并且安装到Vue上：

   ```js
   // 导入 element-ui 这个包
   import ElementUI from 'element-ui'
   // 导入 配套的样式表
   import 'element-ui/lib/theme-chalk/index.css'

   // 把 element-ui 安装到 Vue 上
   Vue.use(ElementUI)
   ```

**按需导入和配置 `Element-UI` (推荐使用这个方式)：**

1. 运行 `npm i babel-plugin-component -D` 安装支持按需导入的模块；

2. 打开 `.babelrc` 配置文件，修改如下：

   ```json
   // 加号为要添加的配置
   {
     "plugins": [
       "transform-runtime",
       + [
       +   "component",
       +   {
       +     "libraryName": "element-ui",
       +     "styleLibraryName": "theme-chalk"
       +   }
       + ]
     ],
     "presets": [
       "env",
       "stage-0"
     ]
   }
   ```




## 使用`vue-cli`快速初始化`vue`项目

```cmd
$ npm i vue-cli -g                // 全局安装脚手架工具
$ vue init webpack project-name   // 初始化项目
$ cd project-name                 // 切换到项目根目录中
$ npm i                           // 安装依赖包
$ npm run dev                     // 一键运行项目
```



### 如何修改项目的运行端口和自动打开浏览器

- 打开 `config -> index.js` 配置文件：

  ```js
  host: '127.0.0.1', 
  port: 3333, 
  autoOpenBrowser: true,
  ```




## ESLint 语法检查规范

1. 声明但是未使用的变量或常量会报错
2. 空行不能连续大于等于2
3. 在行结尾处，多余的空格不允许
4. 多余的分号，不允许
5. 字符串要使用单引号，不能使用双引号
6. 在方法名和形参列表的小括号之间，必须有一个空格
7. 每个文件最后都要有一个空行




## 如何配置VSCode帮我们自动把代码格式化为需要的样子

1. 编译器安装  `Vetur` 插件

2. 编译器安装 `Prettier - Code formatter ` 插件

3. 打开 vs code 的 `文件 -> 首选项 -> 设置`，在`用户设置`最底部的合适位置，添加如下配置：

   ```json
   // 使用 ESLint 规则
   "prettier.eslintIntegration": true,
   // 每行文字个数超出此限制将会被迫换行
   "prettier.printWidth": 165,
   // 使用单引号替换双引号
   "prettier.singleQuote": true,
   // 格式化文件时候，不在每行结尾添加分号
   "prettier.semi": false
   ```

4. 解决 方法形参小括号前面，缺少空格报错的问题, 找到 `.eslintrc.js` 配置文件的 `rules` 节点：

   ```js
   // 方法形参列表小括号 和 function 之间缺少空格，也不报错
   'space-before-function-paren': ['error', 'never']
   ```




## 将项目源码托管到oschina中

[码云官网](https://gitee.com/)
1. 点击头像 -> 修改资料 -> SSH公钥 [如何生成SSH公钥](http://git.mydoc.io/?t=154712)
2. 创建自己的空仓储，使用 `git config --global user.name "用户名"` 和 `git config --global user.email ***@**.com` 来全局配置提交时用户的名称和邮箱
3. 使用 `git init` 在本地初始化项目
4. 使用 `touch README.md` 和 `touch .gitignore` 来创建项目的说明文件和忽略文件；
5. 使用 `git add .` 将所有文件托管到 git 中
6. 使用 `git commit -m "init project"` 将项目进行本地提交
7. 使用 `git remote add origin 仓储地址`将本地项目和远程仓储连接，并使用origin最为远程仓储的别名
8. 使用 `git push -u origin master` 将本地代码push到仓储中




## git中常用的命令

1. `git checkout -b 分支名称` 在当前的分支上使用`-b`新创建一个子分支，并立即使用`checkout ` 切换到自分支
2. `git branch 分支名称` 是单纯的创建一个子分支
3. `git checkout 分支名称` 切换分支
4. 在 `master`分支上，运行 `git merge 子分支名称` ， 就表示说，把 子分支上所有功能代码，合并到主分支；
5. `git status` 查看状态
6. `git add .` 添加到暂存区
7. `git commit -m '消息'` 提交到本地存储中




## 装less-loader时装其依赖less

```cmd
npm i less-loader less -D
```

