## 单页面应用程序

- Single Page Web Application（SPA）
- 从字面意义来看就是一个网站就一个页面
  - coding
  - 网易云音乐
  - 极致用户体验，就像 native app 一样。
- 优点
  - 分离前后端关注点，前端负责界面显示，后端负责数据存储和计算，各司其职，不会把前后端的逻辑混杂在一起
  - 1、具有桌面应用的即时性、网站的可移植性和可访问性。
    2、用户体验好、快，内容的改变不需要重新加载整个页面，web应用更具响应性和更令人着迷。
    3、基于上面一点，SPA相对对服务器压力小。
    4、良好的前后端分离。SPA和RESTful架构一起使用，后端不再负责模板渲染、输出页面工作，web前端和各种移动终端地位对等，后端API通用化。
    5、对前端人员javascript技能要求更高，促使团队技能提升。
  - 我的页面我做主
- 缺点
  - 致命缺点：SEO 问题，搜索引擎优化 , 浏览器很难查询到网页信息 
  - 目前也有一些对应的解决方案：但是都不够完美
  - 1、不利于SEO。
    2、初次加载耗时相对增多。
    3、导航不可用，如果一定要导航需要自行实现前进、后退。
    4、对开发人员技能水平、开发成本高。

### 简单模拟单页面应用程序的效果

#### hashchange事件

- `hash锚点 `

- `window.onhashchange` 事件  

  - 当 hash(就是url #及其后面的部分 )发生变化时就会触发该事件

- jQuery ajax 

- 当 hash 改变的时候，根据不同的 hash 做不同处理

- | hash      | ajax请求       | 网页       |
  | --------- | ------------ | -------- |
  | #/        | find.html    | 主页面      |
  | #/my      | my.html      | 我的(功能界面) |
  | #/friends | friends.html | 朋友(功能界面) |

  ​

- ```javascript

      // 1. 注册 window.onhashchange 事件（当地址中的 hash 改变的时候会触发该事件）
      // 2. 获取 hash 中的地址，然后根据不同的地址，通过 ajax 请求得到局部网页
      // 3. 把得到的局部网页渲染到 container 容器中

      hashchangeHandler()

      window.onhashchange = hashchangeHandler

      function hashchangeHandler() {
        var hash = window.location.hash
        //去掉url地址的 # 号
        var pathname = hash.substr(1)
        if (pathname === '/') {
          // 异步请求显示 find.html
          $.ajax({
            url: './find.html',
            type: 'get',
            success: function (data) {
              $('#container').html(data)
            }
          })
        } else if (pathname === '/my') {
          $.ajax({
            url: './my.html',
            type: 'get',
            success: function (data) {
              $('#container').html(data)
            }
          })
        } else if (pathname === '/friend') {
          // $.ajax({
          //   url: './friend.html',
          //   type: 'get',
          //   success: function (data) {
          //     $('#container').html(data)
          //   }
          // })
          $('#container').html($('#friend_html').html())
        }
      }
    
  ```

  ​