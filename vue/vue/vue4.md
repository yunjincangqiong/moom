# Webpack

## 在网页中会引用哪些常见的静态资源？

1. 样式表
   + .css     .less(Less)     .scss(Sass)
2. JS文件
   + .js        .ts(TypeScript)   .coffee(CoffeeScript)
3. 图片
   + .jpg/.jpeg    .png   .gif    .bmp    .webp(在苹果手机的浏览器中显示不出来)
4. 字体文件
   + .ttf     .eot    .woff    .woff2    .svg
5. 模板文件
   + .vue(Vue)   .jsx(React)
6. 视频文件
   + .mp4   .ogg    .webm    .avi
7. 音频文件
   + .mp3   .ogg  

## 网页中引入的静态资源多了以后有什么问题？？？

1. **对网页性能不友好：**要发起很多的静态资源请求，降低页面的加载效率，用户体验差；
2. **对程序开发不友好：**要处理复杂的文件之间的依赖关系；




## 如何解决上述两个问题

1. 对于 JS 文件 或  CSS 文件，可以合并和压缩；小图片适合转 Base64 格式的编码；
2. 通过一些工具，让工具自动维护文件之间的依赖关系；




## webpack
+ [webpack官网](http://webpack.github.io/)
+ **什么是webpack：**前端项目的构建工具
+ **什么项目适合使用webpack：**
    + 非常适合与单页面应用程序(pwa)结合使用；
    + 不太适合与多页面的普通网站结合使用；
+ **为什么要使用webpack:**
    1. 可以书写高级的js代码，且不用考虑兼容性；
    2. 能够优化项目的性能；
    3. 程序员可以把开发重心放到业务逻辑上；
+ 本篇基于最新的 webpack 4.x 版本




## 在项目中安装和配置`webpack`

1. 新建一个项目的空白目录，并在在终端中，`cd`到项目的根目录，执行`npm init -y` 初始化项目

2. 装包：运行 `cnpm i webpack webpack-cli -D` 安装项目构建所需要的 `webpack` 文件

   + -D : 将包的依赖到 package.json 的 devDependencies 属性中, 代表仅开发中使用

3. 打开 `package.json`文件，在 `scripts` 属性中，新增一个 `dev` 的属性：

   ```json
   // scripts属性用于存贮 npm 的命令, 可以自定义命令, 语法 npm 命令名称 
   "scripts": {
     "start": "npm run dev", // 这是一个自定义命令
     "test": "echo \"Error: no test specified\" && exit 1",
     "dev": "webpack" 
   },
   ```

4. webpack 基于 node.js 开发, 所以，webpack.config.js 配置文件中，支持 Node.js 语法

   这个配置对象的作用：每当大家运行 npm run dev 的时候，都会执行 webpack 命令；当 webpack 工具在转换代码之前，会先读取项目根目录中 webpack.config.js 中导出的配置对象；然后，根据配置对象指定的相关配置，进行代码的转换；

   在项目根目录中，新建一个 `webpack.config.js` 配置文件，内容如下：

   ```js
   // 这是 使用 Node 语法， 向外导出一个 配置对象
   module.exports = {
     // production(生产环境), 会自动压缩代码(上线时使用)
     // development(开发环境), 不会压缩代码, 提高编译速度(开发时使用)
     mode: 'development' // 定义当前的模式
   }
   ```

5. 在项目根目录中，新增一个 `src` 目录，并且，在 `src` 目录中，新建一个 `index.js` 文件，作为 `webpack 构建的入口`；会把打包好的文件输出到根目录下的`dist`目录(如果没有这个目录会自动创建)中的`main.js`文件(如果没有这个文件会自动创建)

   **说明: webpack 4.x 的版本；默认约定： 会把 src -> index.js 进行代码转换；并把 转换好的 代码，输出到 dist -> main.js 的文件中；**

6. 在终端中，直接运行 `npm run dev`  启动 webpack 进行项目构建；




## 实现`webpack`的实时打包构建

**使用该命令工具运行之后, 需要通过本地服务器访问, 默认 localhost:8080**

1. 借助于 `webpack-dev-server` 这个工具，能够实现 webpack 的实时打包构建；

2. 运行`cnpm i webpack-dev-server -D` 安装包

3. 打开`package.json`文件，把 `scripts` 属性下的 `dev` 属性，修改为以下配置：

   ```json
   "scripts": {
     "test": "echo \"Error: no test specified\" && exit 1",
     "dev": "webpack-dev-server"
   },
   ```

4. 修改 `index.html` 文件中的 `script` 的 `src`, 让 `src` 指向 内存中根目录下的 `/main.js`

   **注意：使用 webpack-dev-server 可以实现实时打包；但是，打包的 main.js 并没有像之前那样存放到了 物理磁盘上的 dist -> mian.js； 而是存放到了内存中；我们可以直接 访问项目的根目录，来得到这个  main.js  文件；**

   原因: 内存的存取速度快, 可以延长硬盘的读写寿命

   ```html
   <script src="/main.js"></script>
   ```




## 使用`html-webpack-plugin`插件配置启动页面

该插件的作用: 

+ 自动把 打包好的 main.js 注入到 index.html 页面中
+ 把 磁盘上的 index.html 页面(启动页面)，复制一份并托管到 内存中

使用步骤:

1. 装包`cnpm i html-webpack-plugin -D `

2. 在 `webpack.config.js`中，导入 插件：

   ```js
   const HtmlPlugin = require('html-webpack-plugin')
   const htmlPlugin = new HtmlPlugin({
     // 传递一个配置对象
     template: './src/index.html', // 指定路径，表示 要根据哪个物理磁盘上的页面，生成内存中的页面
     filename: 'index.html' // 指定，内存中生成的页面的名称
   })
   ```

3. 把 创建好的 `htmlPlugin` 对象，挂载到 `plugins`属性中：

   ```js
   module.exports = {
     mode: 'development', // 当前处于开发模式
     // 所有的插件，必须放到 plugins 属性中才能生效
     plugins: [htmlPlugin] // 插件数组
   }
   ```




## 实现自动打开浏览器、热更新和配置浏览器的默认端口号

以下均为 webpack-dev-server 工具的额外配置

+ `--open` 自动打开浏览器 后可跟浏览器名称(中间需要有一个空格)
+ `--host` 配置IP地址 后跟IP地址(中间需要有一个空格)
+ `--port` 配置端口号 后跟端口号(中间需要有一个空格)
+ `--hot` 热更新；最新的代码，以打补丁的形式，替换到页面上，加快编译的速度；(没修改的代码不会重新编译)
+ `--compress` 对网络中传输的文件进行压缩，提高传输效率;
+ `--progress ` 展示编译的进度(无用)


```json
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  // 开发时使用 dev 命令
  "dev": "webpack-dev-server --open --host 127.0.0.1 --port 3000 --hot --compress",
  // 上线时使用 pub 命令, 将打包好的 dist 文件夹直接上交即可
  "pub": "webpack"
}
```



## 打包处理非`js`文件

### 使用webpack打包css文件

1. 运行 `cnpm i style-loader css-loader -D`

2. 打开 `webpack.config.js` 配置文件，在 `module` -> `rules` 数组中，新增处理 css 样式表的loader规则：

   **use 属性里面的 loader 顺序一定不能改变**

   ```json
   module: { // 所有 非.js 结尾的第三方文件类型，都可以在 module 节点中进行配置处理
     rules: [ // rules 是匹配规则，如果 webpack 在打包项目的时候，发现，某些 文件的后缀名是 非 .js 结尾的, 此时，webpack 就会查找 配置文件中的 module -> rules 规则数组；
       // test: 为一个正则表达式, 匹配相应的文件后缀
       // use: 为匹配到的文件应用相应的 loader 来解析打包; 应用 loader 的顺序为从后往前依次应用
       // 具体到这行就是先应用 css-loader 在应用 style-loader, 顺序不对会报错
       { test: /\.css$/, use: ['style-loader', 'css-loader'] }
     ]
   }
   ```




### 使用webpack打包less文件

1. 运行 `cnpm i less-loader less -D`

   + **注意: less 为 less-loader 依赖的一个文件不用特殊处理**

2. 在 webpack 的配置文件中，新增一个 rules 规则来 处理 less 文件：

   ```json
   { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }
   ```




### 使用webpack打包sass文件

1. 运行 `cnpm i sass-loader node-sass -D`

   + **注意: node-sass 为 sass-loader 依赖的一个文件不用特殊处理**

2. 在 webpack 的配置文件中，新增一个 rules 规则来 处理 scss文件：

   ```json
   { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
   ```




### 使用webpack处理css中的路径

1. 运行 `cnpm i url-loader file-loader -D`

   + **注意: file-loader 为 url-loader 依赖的一个文件不用特殊处理**

2. 在 webpack 的配置文件中，新增一个 rules 规则来 处理 图片 文件：

   会将图片编译为 base64 格式

   好处: 减少一次 http 请求, 增加访问速度

   ```js
   { test: /\.(jpg|png|gif|bmp)$/, use: 'url-loader' }
   ```

3. 新增一个 rules 规则来 处理 字体 文件：

   ```js
   { test: /\.(eot|ttf|woff|woff2|svg)$/, use: 'url-loader' }
   ```

   ​





### 使用babel处理高级JS语法

[babel-preset-env：你需要的唯一Babel插件](https://segmentfault.com/p/1210000008466178)
[Runtime transform 运行时编译es6](https://segmentfault.com/a/1190000009065987)

1. 之前说过，webpack 默认能够打包处理一些ES6中的高级语法；但是，webpack 并不能处理所有的高级ES6, ES7语法；

2. 运行两套命令，去安装相关的 loader:

   + 运行 `cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`
   + 运行 `cnpm i babel-preset-env babel-preset-stage-0 -D`
     + babel-preset-env 根据配置的目标运行环境自动启用需要的 babel 插件, 并根据配置的 env 只编译那些还不支持的特性
     + stage-0 是对ES7一些提案的支持，Babel通过插件的方式引入，让Babel可以编译ES7代码。

3. 添加 babel-loader 配置项：

   ```js
   // 注意：在配置 babel-loader 的时候，一定要添加 exclude 排除项，把 node_modules 目录排除
   // 这样，只让 babel-loader 转换 程序员 自己手写的 JS 代码；
   // 好处：1. 能够提高编译的转换效率； 2. 能够防止不必要的报错！
   { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
   ```

4. 在项目根目录中，创建 `.babelrc` json文件配置文件并写入以下内容:

   ```json
   {
     "presets": ["env", "stage-0"],
     "plugins": ["transform-runtime"]
   }
   ```




## 在webpack中使用bootstrap

由于其依赖 jQuery, 所以需要先引入并配置jQuery

在 webpack.config.js 中, 导入 webpack, 并配置jQuery, 在添加到 plugins 中

```js
const Webpack from 'webpack'
const jquweyPlugin = new Webpack.ProvidePlugin({
  $: "jquery",
  jQuery: "jquery"
})
module.exports = {
  plugins: [其他插件配置, jquweyPlugin]
}
```

在 index.js 中引入 bootstrap 即可

```js
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.js.css'
```



## 样例完整的 webpack.config.js 文件配置

```js
const HtmlPlugin = require('html-webpack-plugin')
const htmlplugin = new HtmlPlugin({
  template: './src/index.html', 
  filename: 'index.html' 
})

module.exports = {
  mode: 'development', 
  plugins: [htmlplugin], 
  module: { 
    rules: [ 
      { test: /\.css$/, use: ['style-loader', 'css-loader'] },
      { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
      { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
      { test: /\.(jpg|png|gif|bmp)$/, use: 'url-loader' },
      { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
    ]
  }
}
```



## ES6中的模块化语法

[es6模块化参考文献](http://es6.ruanyifeng.com/#docs/module)

模块化命令可以出现在模块的任何位置，只要处于模块全局作用域(顶级作用域)就可以. 不能写在块级作用域中.

### export

`export`语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值。

export 将模块内的变量导出

```js
// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
// 对n起一个别名
export {n as m};
```

export 将模块内的函数导出

```js
// 写法一
export function f() {};

// 写法二
function f() {}
export {f};
```



### export default

同一个文件中只能只用一次

使用 export default 向外暴露的成员，可以使用任何合法的名称来接收, 并且不用使用 {}

```js
import ssd from module
```

export default 支持下面的写法

```js
function fn() {}
export default fn
```

不支持以下写法

```js
export default var a = 1;
```

其余语法与 export 大都相同



### import

自己写的 js模块文件 可以使用 相对路径 或 绝对路径 来引入

使用 export 向外暴露的成员，需要使用 import {} from '文件名/模块名' 来接收; 

export 向外暴露的成员，必须严格按照导出的名称，来使用 {} 进行接收；

```js
// test.js
export var lastName = 'ssd'
// index.js
// 可以通过 as 对变量起别名, 这样原名就不生效了
import { lastName as surname } from './test.js';
```

`import`命令导入的变量都是只读的, 如果导入的时对象, 则可以更改其属性, 但是不建议这样做. 会产生很多问题. 建议凡是输入的变量，都当作完全只读，轻易不要改变它的属性。

**注意，`import`命令具有提升效果，当前行会提升到整个模块的头部，首先执行。**

由于`import`是静态执行，所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构。

```js
// 报错
import { 'f' + 'oo' } from 'my_module';

// 报错
let module = 'my_module';
import { foo } from module;

// 报错
if (x === 1) {
  import { foo } from 'module1';
} else {
  import { foo } from 'module2';
}
```

上面三种写法都会报错，因为它们用到了表达式、变量和`if`结构。在静态分析阶段，这些语法都是没法得到值的。

`import`语句会执行所加载的模块, 所以在模块文件不需要导入变量的时候可以简写

```js
import module;
```

如果多次重复执行同一句`import`语句，那么只会执行一次，而不会执行多次。

多种 模块化语言 不要同时存在

