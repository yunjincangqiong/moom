# AMD

js模块化的一个规则, 类似的还有CMD, UMD 

## require.js

作为AMD规则的一个实例化的插件

RequireJS的目标是鼓励代码的模块化，它使用了不同于传统 <script>标签的脚本加载步骤。可以用它来加速、优化代码，但其主要目的还是为了代码的模块化。它鼓励在使用脚本时以module ID替代URL地址。

### 插件加载和baseUrl

RequireJS以一个相对于[baseUrl](http://makingmobile.org/docs/tools/requirejs-api-zh/#config-baseUrl)的地址来加载所有的代码。 引入插件的<script>标签含有一个特殊的属性data-main，require.js使用它来启动脚本加载过程，而baseUrl一般设置到与该属性相一致的目录。下列示例中展示了baseUrl的设置：

```html
<script data-main="scripts/main.js" src="scripts/require.js"></script>
```

### 声明模块

声明模块使用 define 关键字声明模块

```javascript
// 无依赖项的模块声明
define(function () {
	功能代码;
})
// 如果该模块有依赖项, 将该模块依赖的模块通过第一个可选数组参数导入
// 默认假定所有的依赖资源都是js脚本，因此无需在module ID上再加".js"后缀
define(['../a', '../c', 'test/e'], function () {
	功能模块;
})
```

