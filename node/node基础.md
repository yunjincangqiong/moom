### 从0开始创建一个完整的node项目

```
1.创建一个项目目录
2.在项目目录打开cmd
3.npm init   初始化node项目文件  会一步一步提示输入项目的信息 并且在根目录下生成一个 package.json 文件 存放项目的各种信息 (注意每个项目都应该有一个 package.json 文件)
  npm init -y  快捷生成项目文件, 所有信息都为默认值
4.创建 views目录 存放 html 文件等静态文件
5.创建 public 目录 存放用户可访问的文件
6.npm i -S 包名  创建一个 node_module 目录用于存放所有包文件, 下载包文件到node_module 目录 并且将 包信息 自动添加到package.json文件中
格式如下	"dependencies": {
    	      "art-template": "^4.12.2",
    		  "jquery": "^3.2.1"
            }
```

### 重点

```
node为提供js代码运行在后台服务器中的平台, 并且提供一些服务器端的模块文件
node中没有 DOM ,BOM 也就是说没有 window document 对象
注意响应信息完毕时一定要 res.end() 结束响应
文件模块读取文件时为2进制或者16进制数据, 要作为字符串使用时及得转义
发送中文数据时, 注意编码格式
```

### 语法风格

```
在使用无逗号写法时 注意以下三点
[ ( `  在有以上三个字符开头的语句中,需要在语句前面加上一个 ; 分号
样例 :
;[1,2,2,3].foreach(function(item){})  
;(function(){
	
})()
//es6语法多行字串  在其中可使用 ${ 变量名 } 来获取变量名的值
var name = 'wang'
`<tr>
	<td>${ name }</td>
 </tr>
`.indexOf()
```

### node自带成员

```
require   加载模块   可以加载内置的模块  也可以加载自定义的模块文件 还可以加载第三方模块文件

exports   导出数据对象 一般使用在自定义模块文件中 在一个模块文件中如果要将数据共享给引用他的文件就需要将共享的数据挂载在exports对象下面
exports.name = 'wang'
另一个引用文件使用时: 
var zd = require('文件路径可无后缀名')
zd.name // wang

__dirname(常用) 和 __filename
在每个模块中，除了 require、exports 等模块相关 API 之外，还有两个特殊的成员：
- __dirname 动态获取 可以用来获取当前文件模块所属目录的绝对路径
- __filename 动态获取 可以用来获取当前文件的绝对路径
- __dirname 和 __filename 是不受执行 node 命令所属路径影响的
在文件操作中，使用相对路径是不可靠的，因为在 Node 中文件操作的路径被设计为相对于执行 node 命令所处的路径（不是bug，人家这样设计是有使用场景）。
所了为了解决这个问题，很简单，只需要把相对路径变为绝对路径就可以了。
那这里我们就可以使用 __dirname 或者 __filename 来帮我们解决这个问题了。
在拼接路径的过程中，为了避免手动拼接带来的一些低级错误，所以推荐多使用：path.join() 来辅助拼接。注意需要加载path模块
所以为了尽量避免刚才所描述这个问题，大家以后在文件操作中使用的相对路径都统一转换为 动态的绝对路径。
补充：模块中的路径标识和这里的路径没关系，不受影响（相对于文件模块）
```

### node常用API

```
//文件操作模块
var fs = require('fs')
//以下函数在请求成功时 err 为 null ; data 为获取到的数据
//以下函数在请求成功时 err 为 错误信息 ; data 为 undefined
fs.readFile('文件名',function(err, data){})     读取文件
//注意如果写入一个不存在的文件时 会创建这个文件并且把内容写进去 会覆盖文件中的内容
fs.writeFile('文件名','写入文件的内容',function(err){})	 写入文件
//files 为数组
fs.readDir('文件名',function(err, files){})	 读取文件目录

//http模块 
var http = require('http')
http.createServer(function(req,res){
  req.url                                    用户输入的url地址
  res.statusCode = 302     					相应状态码 : 页面重定向
  res.setHeader('Location','地址url')		   设置响应头 地址栏url地址
  res.end(可选参数:发送的数据)                 响应结束
}).listen('3000',function(){})

//url模块
var url = require('url')
//解析一个url地址 第二个参数为 true 时,query属性解析为对象
var urlPath = url.parse('/pinglun?name=wang&age=18',true)
urlPath.pathname   // /pinglun  获取url中的相对文件路径
urlPath.query	   // {"name":"wang","age":18}

//Path模块
//最常用
- path.join(__dirname + './文件名')
  - 当你需要进行路径拼接的时候，推荐使用这个方法
  
- path.basename
  - 获取一个路径的文件名（默认包含扩展名）
- path.dirname
  - 获取一个路径中的目录部分
- path.extname
  - 获取一个路径中的扩展名部分
- path.parse
  - 把一个路径转为对象
    - root 根路径
    - dir 目录
    - base 包含后缀名的文件名
    - ext 后缀名
    - name 不包含后缀名的文件名
- path.isAbsolute 判断一个路径是否是绝对路径

```

### 一个基本的服务器创建流程

~~~
//加载http模块
var http = require('http')
//创建一个服务器连接
var server = http.createServer()
//监听服务的请求事件
server.on('request',function(req, res){
  req.url 请求的url地址(为相对地址 默认为 /)
  res.end(相应给用户的信息)
})
server.listen('服务器端口号',function(){
  连接服务器成功返回的信息
})
~~~

### 创建一个基本的服务器创建流程(简写)

```
//加载http模块
var http = require('http')
//创建一个服务器连接并监听客户端的请求事件 相当于链式编程(前一个函数的返回值正好是下一个函数的调用对象)
http
  .createServer(function(req, res){
  req.url 请求的url地址(为相对地址 默认为 /)
  res.end(相应给用户的信息)
})
  .listen('服务器端口号',function(){
  连接服务器成功返回的信息
})
```

### 服务器端模板引擎的用法

```
//在相应的目录下载art-template模块
npm install art-template
//加载模块
var template = require('art-template')
//!!!!!!!!!!!!注意!!!!!!!!!!
//如果没有下载模块就要引用外部文件模块
var template = require('./art-template')

var fs = require('fs')
//以字符串格式读取模板文件
fs.readFile('模板文件路径',function(err, data){
  if(err){
    return console.log('404')
  }
  var htmlTemplate = template.render(data.toString(),{
    模板引擎对象
  })	
  res.end(htmlTemplate)
})

模板引擎文件写法
不用引用art-template文件
在要插入模板的位置直接写模板格式即可
例如: 在表格中插入数据 原生语法
<tbody id="tbody">
    <% for(var i = 0;i < files.length;i++) {%>
      <tr><td><a href="#"><%= files[i] %>/</a></td></tr>
    <% } %>
</tbody>
知识简单的遍历可以使用简介语法
说明 $value 为对象的值 $name 为对象的键
<tbody id="tbody">
    {{ each files }}
      <tr><td><a href="#">{{ $value }}/</a></td></tr>
    {{ /each }}
    {{ if 条件 }}
    {{ else }}
    {{ /if }}
</tbody>
```

### cmd基本指令

```
cls   清屏
dir   文件目录
cd    切换路径
mkdir 创建文件夹(目录)
ipconfig  计算机IP信息
ctrl + c 结束当前服务
xxx -v 查看当前版本号  可用于判断当前插件或者软件有没有安装
```

### npm

```
全称 : 
node package manager  npm包管理工具

自升级到最新版本 :
npm install --global npm

常用命令 :
//说明 在无意间删除node_module文件夹时 通过此命令可将 包文件 一次下载回来 
(前提 使用npm i -S 包名  命令)
npm install  根据 package.json 依赖下载包文件
  npm i    简写

npm init   初始化项目文件
  npm init -y   快速初始化, 跳过信息填写所有值都为默认值
npm install 包名   只下载包文件  不推荐使用
  npm i 包名   简写
npm install --save 包名  下载包文件并存贮依赖信息  强烈建议使用
  npm i -S 包名  简写
npm uninstall 包名   删除文件但是不删除依赖
  npm un 包名   简写
npm uninstall --save 包名  删除文件及其依赖
  npm un -S 包名  简写
在cmd中输入指令 node + 回车 可模拟node运行环境(与 chrome 控制台相似)
执行文件时 在当前文件打开cmd  输入指令 npm 文件名
```

#### package.json 和 package-lock.json(了解)

npm init 会自动生成package.json文件

npm 5 以前是不会有 `package-lock.json` 这个文件的。

npm 5 以后才加入了这个文件。

当你安装包的时候，npm 都会生成或者更新 `package-lock.json` 这个文件。

- npm 5 以后的版本安装包不需要加 `--save` 参数，它会自动保存依赖信息
- 当你安装包的时候，会自动创建或者是更新 `package-lock.json` 这个文件
- `package-lock.json` 这个文件会保存 `node_modules` 中所有包的信息（版本、下载地址）
  - 这样的话重新 `npm install` 的时候速度就可以提升
- 从文件来看，有一个 `lock` 称之为锁
  - 这个 `lock` 是用来锁定版本的
  - 如果项目依赖了 `1.1.1` 版本
  - 如果你重新 isntall 其实会下载最新版本，而不是 1.1.1
  - 我们的目的就是希望可以锁住 1.1.1 这个版本
  - 所以这个 `package-lock.json` 这个文件的另一个作用就是锁定版本号，防止自动升级新版

### 加载项目所需要的文件资源

```
默认情况下不会加载任何文件或者插件
一般来说在项目文件中会有一个public文件夹 在里面存放着可以公开请求的文件和插件
还有一个 views 文件夹存放 html 页面
判断用户请求的url  如果为某个特定的路径(/public/) 就可以允许用户(或者文件导入插件的连接)访问其中的文件
注意!!!!!文件的相对路径(./ ../)和用户的请求url地址(/根目录)之间的区别
样例 : 
if(req.url.indexOf('/public/') === 0){
  fs.readFile('.' + req.url,function(err, data){
    if(err){
     return console.log('404')
    }
    res.end(data)
  })
}
```

### 模块系统和原理

```
node 中的模块 分为三种 核心模块 第三方模块 自定义模块 
其中第三方模块 需要 自己下载 使用npm命令 npm i -S 模块名    模块名可以在npm官网查到
正常情况下模块之间无法传递函数和变量;相当于每个模块都是一个封闭的空间;互不影响

原理 : 
每个 node 模块文件中都定义了一个 module 对象 ; 这个对象下面还有一个 exports 属性也是一个对象
var module = { exports : {} }
所有挂载在 module.exports 下面的属性或者方法就可通过 require 方法获取到

官方提供了一个额外的变量 exports 来代替 module.exports
var exports = module.exports  
也就是说 这两个变量指向相同的域 在挂载变量或者函数时都会改变域的存贮值

在每个文件的最后 都要将 (!!!!!!)module.exports(!!!!!!) 返回 ; 也就是说谁 require 模块文件 谁就得到 module.exports 里面的值
return module.exports

特殊 :
因为都是变量所以在 重新赋值时就会失去原来的指针 使两个变量之间的关联断开
但是可以使用 exports = module.exports 的方法来使两个变量恢复关联关系

导出值 :
在需要导出多个值时 将值挂载在 module.exports 或者 exports 上
推荐使用第二中方法
module.exports.add = function(){} 或者 exports.add = function(){} 
在需要导出单个值时 重新给 module.exports 赋值即可
module.exports = [1,2,3,4]
```

### require原理

```
两个作用：
- 执行被加载模块中的代码
- 得到被加载模块中的 module.exports 导出接口对象
require 为模块加载函数
require 已经加加载过的文件不会去重复加载 再次使用时只会拿到其中的接口对象

核心模块 :
核心模块的本质也是文件, 并且已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了
var http = require('http')
常用的核心模块
fs      文件操作 
http    服务的 
url     url操作
path    路径处理
os      操作系统信息

自定义模块 :
加载时为文件路径方式 推荐相对路径方式
./当前文件目录下 ../返回上一级目录  两者均不可省略
var exm = require('自定义文件路径')

第三方模块 :
下载后使用  使用npm命令下载后会在当前项目目录下自动生成一个 node_modules 文件夹, 所有下载的第三方包都在这里面, 不可能有任何一个第三方包和核心模块的名字是一样的
注意：我们一个项目有且只有一个 node_modules，放在项目根目录中，这样的话项目中所有的子目录中的代码都可以加载到第三方包

加载时使用 包名 即可
var jquery = require('jquery')

加载机制 :
1.先找到当前文件所处目录中的 node_modules 文件夹
2.在文件夹中找到相应的 包 
3.在包中找一个 package.json 的文件
4.在 package.json 文件中找到 main 属性
5.main 中就记录了 包 的入口文件(一般为index.js)
6.如果没有main属性或者package.json文件就在目录中寻找 index.js 文件
7.如果上述条件都不成立, 就往上级查找 重复 1-6 步
8.如果直到当前磁盘根目录还找不到，最后报错：can not find module xxx
```

### express

```
1.npm 命令下载安装
2.引包  var express = require('express')
3.创建一个node服务  var add = express()

常用API : 
公开指定目录
可以通过指定url访问项目指定目录中的文件
app.use('url', express.static('文件目录'))
例: app.use('/public/', express.static('./public/'))

获取的指定url(get请求方式)并执行回调函数
app.get('url',function(req, res){
  req.query 以对象形式获取get请求的键值对信息
  res.send('响应信息')
})

绑定并监听服务器端口信息
app.listen('端口号',function(){
  连接成功时返回的信息
})

使用模板引擎(art-template)

```

### http-server

```
是一个基于 node.js , 简单的，零配置的命令行http服务器。
npm i http-server -g 全局安装
在此电脑中配置用户环境变量  path  中添加  npm 的绝对url 例 C:\Users\macbook\AppData\Roaming\npm
在需要创建服务器的地方 输入 命令  hs -o 即可
更多详细命令  
https://www.npmjs.com/package/http-server
```



### 修改完代码自动重启

我们这里可以使用一个第三方命名航工具：`nodemon` 来帮我们解决频繁修改代码重启服务器问题。

`nodemon` 是一个基于Node.js 开发的一个第三方命令行工具，我们使用的时候需要独立安装：

```shell
# 在任意目录执行该命令都可以
# 也就是说，所有需要 --global(全局安装) 来安装的包都可以在任意目录执行
npm install --global nodemon
```

安装完毕之后，使用：

```shell
nodemon app.js
```

只要是通过 `nodemon 入口文件名` 启动的服务，则它会监视你的文件变化， 当文件发生变化的时候，自动帮你重启服务器。

### 解决npm被墙问题(了解)

npm 存储包文件的服务器在国外，有时候会被墙，速度很慢，所以我们需要解决这个问题。

http://npm.taobao.org/ 淘宝的开发团队把 npm 在国内做了一个镜像备份。

安装淘宝的 cnpm：

```shell
# 在任意目录执行都可以
# --global 表示安装到全局，而非当前目录
# --global 不能省略，否则不管用
npm install --global cnpm
```

接下来你安装包的时候把之前的 `npm` 替换成 `cnpm`。

举个例子：

```shell
# 这里还是走国外的 npm 服务器，速度比较慢
npm install jquery

# 使用 cnpm 就会通过淘宝的服务器来下载 jquery
cnpm install jquery
```

如果不想安装 `cnpm` 又想使用淘宝的服务器来下载：

```shell
npm install jquery --registry=https://registry.npm.taobao.org
```

但是每一次手动这样加参数很麻烦，所我们可以把这个选项加入配置文件中：

```shell
# 配置到淘宝服务器
npm config set registry https://registry.npm.taobao.org

# 查看 npm 配置信息
npm config list
```

只要经过了上面命令的配置，则你以后所有的 `npm install` 都会默认通过淘宝的服务器来下载。

