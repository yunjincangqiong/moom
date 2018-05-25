# Node 综合 Web 案例

## 目录结构

```
.
├── app.js				项目的入口文件
├── controllers
├── models				存储使用 mongoose 设计的数据模型
├── node_modules 		第三方包(开放性资源)
├── package.json 		包描述文件(自动生成)
├── package-lock.json 	第三方包版本锁定文件（npm 5 以后才有 自动生成）
├── public 				公共的静态资源(开放性资源)
├── README.md 			项目说明文档
├── routes				如果业务比较多，代码量大，最好把路由按照业务的分类存储到 routes 目录中
├── router.js			简单一点把所有的路由都放到这个文件
└── views 				存储视图目录(html视图模板文件)
```

## 模板页

- [art-template 子模板](https://aui.github.io/art-template/zh-cn/docs/syntax.html#子模板)
- [art-template 模板继承](https://aui.github.io/art-template/zh-cn/docs/syntax.html#模板继承)

## 路由设计

简单来说就是针对不同的url和请求方式给与不同的回应

| 路径        | 方法   | get 参数 | post 参数                 | 是否需要登陆 | 备注     |
| --------- | ---- | ------ | ----------------------- | ------ | ------ |
| /         | GET  |        |                         |        | 渲染首页   |
| /register | GET  |        |                         |        | 渲染注册页面 |
| /register | POST |        | email、nickname、password |        | 处理注册请求 |
| /login    | GET  |        |                         |        | 渲染登陆页面 |
| /login    | POST |        | email、password          |        | 处理登陆请求 |
| /logout   | GET  |        |                         |        | 处理退出请求 |



## 模型设计

在实现登录和注册错误处理时使用json数据格式统一处理{err_code:0,err_msg:err}

## 功能实现

## 书写步骤

- 创建目录结构
- 整合静态页-模板页
  - include
  - block
  - extend
- 设计用户登陆、退出、注册 的路由
- 用户注册
  - 先处理好客户端页面的内容（表单控件的 name、收集表单数据、发起请求）
  - 服务端
    - 获取客户端表单请求数据
    - 操作数据库
    - 如果有错，发送 500 告诉客户端服务器错了
    - 其它的根据你的业务发送不同的响应数据
- 用户登陆
- 用户退出