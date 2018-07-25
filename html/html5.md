## DOM扩展

**Node 指一个有效的 DOM 节点，是一个通称。**

### 获取元素

```html
1、document/Node.getElementsByClassName('className') 通过类名获取元素，以伪数组形式存在。获取不到元素时返回空的伪数组

以下两个方法获取不到元素时, 返回 null
Node 方式获取元素内部实现有问题, 所以建议使用 document 方式
2、document/Node.querySelector('selector') 通过CSS选择器(css3)获取元素，返回符合匹配条件的第1个元素。
3、document/Node.querySelectorAll('selector') 通过CSS选择器(css3)获取元素，以伪数组形式存在, 自带 foreach 方法(与数组的 foreach 方法类似)
```

### 类名操作

```html
1、Node.classList.add('class')        添加class
2、Node.classList.remove('class')     移除class
3、Node.classList.toggle('class')     切换class，有则移除，无则添加
4、Node.classList.contains('class')   检测是否存在class
```

### 自定义属性

html5 之前自定义属性没有统一的书写规定, html5 之后规定了自定义属性的定义方式

+ 格式: data-*="自定义属性值"
  + 例如: <div data-info="msg" data-my-name="gt"></div>
+ 获取节点的全部自定义属性, 其值为一个对象, 键为去除 data- 头后的值, 多个 - 连接时, 需要使用驼峰格式
  + Node.dataset    //  {'info': 'msg', 'mYname': 'gt'}
+ 获取节点的指定自定义属性
  + Node.dataset['info']    //  'msg'
+ 设置指定节点的指定自定义属性的值
  + Node.dataset['info'] = 'newmsg'

## 新增API

### 全屏方法

> HTML5规范允许网页上任一元素全屏显示。

- 开启全屏显示   

  - 元素对象.requestFullScreen() 

- 关闭全屏显示  

  -  document.cancelFullScreen() 
  -  由于其兼容性原因，不同浏览器需要添加前缀如：
    Webkit内核浏览器：webkitRequestFullScreen、webkitCancelFullScreen，如chrome, safari
    Gecko内核浏览器：mozRequestFullScreen、mozCancelFullScreen，如火狐浏览器。

- 获取处于全屏的元素, **当前并不是所有的浏览器都支持这个方法**

  - document.fullscreenElement   可以用于检测当前是否处于全屏模式

  - 如果当前没有处于全屏模式, 返回值为 null

  - 如果当前处于全屏, 返回处于全屏模式的元素对象

  - 不同浏览器需要添加前缀 :

    Webkit内核浏览器：document.webkitFullscreenElement  如chrome, safari

    Gecko内核浏览器： document.mozFullScreenElement   如火狐浏览器

#### 对象检测技术

```javascript
// 当前对象如果没有此方法或者属性, 就会返回 undefined
if (document.webkitCancelFullScreen) {
  document.webkitCancelFullScreen();
} else if (document.mozCancelFullScreen) {
  document.mozCancelFullScreen();
}
```

### 媒体对象-Video

#### 简介

html5 提供的视频播放元素

```html
<!-- 基本使用 -->
<video src="./video/chrome.mp4" poster="./images/poster.jpg">
  不支持 video 元素的浏览器会显示这里面的文字
</video>
```

| 属性       | 值类型                        | 值      |
| -------- | -------------------------- | ------ |
| src      | 文件路径, 支持格式为 mp4, ogg, webm | 视频文件路径 |
| poster   | 图片路径                       | 视频封面   |
| loop     | boolean, 默认为 false         | 循环播放   |
| preload  | boolean, 默认为 false         | 视频预加载  |
| autoplay | boolean, 默认为 false         | 视频自动播放 |
| controls | boolean, 默认为 false         | 视频控件   |

> 自定义播放器API

#### 方法

| 方法             | 描述                   |
| -------------- | -------------------- |
| addTextTrack() | 向音频/视频添加新的文本轨道       |
| canPlayType()  | 检测浏览器是否能播放指定的音频/视频类型 |
| load()         | 重新加载音频/视频元素          |
| play()         | 开始播放音频/视频            |
| pause()        | 暂停当前播放的音频/视频         |

#### 属性

| 属性                  | 描述                                   |
| ------------------- | ------------------------------------ |
| audioTracks         | 返回表示可用音轨的 AudioTrackList 对象          |
| autoplay            | 设置或返回是否在加载完成后随即播放音频/视频               |
| buffered            | 返回表示音频/视频已缓冲部分的 TimeRanges 对象        |
| controller          | 返回表示音频/视频当前媒体控制器的 MediaController 对象 |
| controls            | 设置或返回音频/视频是否显示控件（比如播放/暂停等）           |
| crossOrigin         | 设置或返回音频/视频的 CORS 设置                  |
| currentSrc          | 返回当前音频/视频的 URL                       |
| **currentTime**     | **设置或返回音频/视频中的当前播放位置（以秒计）**          |
| defaultMuted        | 设置或返回音频/视频默认是否静音                     |
| defaultPlaybackRate | 设置或返回音频/视频的默认播放速度                    |
| **duration**        | **返回当前音频/视频的长度（以秒计）**                |
| **ended**           | **返回音频/视频的播放是否已结束**                  |
| error               | 返回表示音频/视频错误状态的 MediaError 对象         |
| loop                | 设置或返回音频/视频是否应在结束时重新播放                |
| mediaGroup          | 设置或返回音频/视频所属的组合（用于连接多个音频/视频元素）       |
| muted               | 设置或返回音频/视频是否静音                       |
| networkState        | 返回音频/视频的当前网络状态                       |
| paused              | 设置或返回音频/视频是否暂停                       |
| playbackRate        | 设置或返回音频/视频播放的速度                      |
| played              | 返回表示音频/视频已播放部分的 TimeRanges 对象        |
| preload             | 设置或返回音频/视频是否应该在页面加载后进行加载             |
| readyState          | 返回音频/视频当前的就绪状态                       |
| seekable            | 返回表示音频/视频可寻址部分的 TimeRanges 对象        |
| seeking             | 返回用户是否正在音频/视频中进行查找                   |
| src                 | 设置或返回音频/视频元素的当前来源                    |
| startDate           | 返回表示当前时间偏移的 Date 对象                  |
| textTracks          | 返回表示可用文本轨道的 TextTrackList 对象         |
| videoTracks         | 返回表示可用视频轨道的 VideoTrackList 对象        |
| volume              | 设置或返回音频/视频的音量                        |

#### 事件

| 事件             | 描述                     |
| -------------- | ---------------------- |
| abort          | 当音频/视频的加载已放弃时          |
| **canplay**    | **当浏览器可以播放音频/视频时**     |
| canplaythrough | 当浏览器可在不因缓冲而停顿的情况下进行播放时 |
| durationchange | 当音频/视频的时长已更改时          |
| emptied        | 当目前的播放列表为空时            |
| **ended**      | **当目前的播放列表已结束时**       |
| **error**      | **当在音频/视频加载期间发生错误时**   |
| loadeddata     | 当浏览器已加载音频/视频的当前帧时      |
| loadedmetadata | 当浏览器已加载音频/视频的元数据时      |
| loadstart      | 当浏览器开始查找音频/视频时         |
| pause          | 当音频/视频已暂停时             |
| play           | 当音频/视频已开始或不再暂停时        |
| playing        | 当音频/视频在已因缓冲而暂停或停止后已就绪时 |
| progress       | 当浏览器正在下载音频/视频时         |
| ratechange     | 当音频/视频的播放速度已更改时        |
| seeked         | 当用户已移动/跳跃到音频/视频中的新位置时  |
| seeking        | 当用户开始移动/跳跃到音频/视频中的新位置时 |
| stalled        | 当浏览器尝试获取媒体数据，但数据不可用时   |
| suspend        | 当浏览器刻意不获取媒体数据时         |
| **timeupdate** | **当视频的播放位置更改时**        |
| volumechange   | 当音量已更改时                |
| waiting        | 当视频由于需要缓冲下一帧而停止        |

### 地理定位

#### 简介

> 在HTML5规范中，增加了获取用户地理信息的API，
> 这样使得我们可以基于用户位置开发互联网应用，
> 即基于位置服务 (Location Base Service)

地理坐标获取默认是由 google 的一个网站提供, 由于历史原因, 国内不能访问国外的网站(防火墙), 但是可以使用 vpn 等方式翻墙访问, 但由于 vpn 不是还嫩普及, 所以 html5 提供的地理定位使用较少

电脑定位用的是IP地址, 手机使用的位置服务

- 获取当前地理信息

```
window.navigator.geolocation.getCurrentPosition(successCallback, errorCallback) 
```

- 重复获取当前地理信息

```
window.navigator.geolocation.watchPosition(successCallback, errorCallback)
```

- 当成功获取地理信息后，会调用succssCallback，该回调函数有一个形参 position 为包含位置信息的对象。
  + position.coords.longitude 经度
  + position.coords.latitude 纬度
- 当获取地理信息失败后，会调用errorCallback，该回调函数有一个形参 error 包含错误信息 error.message

现实开发中: 

- 通过调用第三方API（[如百度地图](http://lbsyun.baidu.com/index.php?title=jspopular)）来实现地理定位信息，这些API都是基于用户当前位置的，并将用位置位置（经/纬度）当做参数传递，就可以实现相应的功能。

#### 样例-结合百度地图API

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Hello, World</title>
    <style type="text/css">
    html {
        height: 100%
    }

    body {
        height: 100%;
        margin: 0px;
        padding: 0px
    }

    #container {
        height: 100%
    }
    </style>
    <!-- 向百度地图发送请求 -->
  	<!-- v2.0版本的引用方式：src="http://api.map.baidu.com/api?v=2.0&ak=您的密钥" -->
    <script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=0A5bc3c4fb543c8f9bc54b77bc155724"></script>
</head>

<body>
	<!-- 存放地图的容器 -->
    <div id="container"></div>
    <script type="text/javascript">
    	navigator.geolocation.getCurrentPosition(function(position) {
	       // 创建百度地图实例  
		   var map = new BMap.Map("container");  	
		   // 创建点坐标, 传入返回的经度, 纬度坐标值(数值型)
		   var point = new BMap.Point(position.coords.longitude, position.coords.latitude);
		   // 初始化地图，设置中心点坐标和地图级别
		   map.centerAndZoom(point, 18);
    	}, function (error) {
    	   console.log(error);
    	});
    	// 创建自定义地图标注 并添加到地图中
    	var myIcon = new BMap.Icon("marker.png", new BMap.Size(256, 256));  
    	var marker = new BMap.Marker(point, {icon: myIcon});
    	map.addOverlay(marker);
    	map.addEventListener('click', function (e) {
    		console.log(e);
    	}); 
    </script>
</body>

</html>
```

### 文件读取

#### 简介

**不用借助于后端就可以读取用户选择的文件**

用来读取 <input type="file"> 文件选择框中选择的文件

通过 FileReader 构造函数创建文件读取对象，调用文件读取对象下面的方法以实现文件读取的目的。使用方式类似于 XMLHttpRequest 构造函数

用途: 常用于上传图片即时预览。

#### 方法

| 方法名             | 用途                       |
| --------------- | ------------------------ |
| readAsText()    | 读取文本文件。                  |
| readAsDataURL() | 读取文件，返回文件的代码表示方式，通常用于图片。 |

#### 属性

+ result
  + 读取文本文件时为读取到的文本信息
  + 读取图片时为图片的 base64 格式的编码

#### 事件

| 事件名称        | 含义                |
| ----------- | ----------------- |
| onload      | 文件读取完成时           |
| onabort     | 文件读取中断时           |
| onerror     | 文件读取错误时           |
| onloadstart | 文件开始读取时           |
| onloadend   | 文件读取完成时（无论成功或者失败） |
| onprogress  | 文件读取过程中持续触发       |

#### 使用步骤

```text
1.创建文件读取对象
var reader = new FileReader();

2.读取文件 将文件内容以代码的方式返回
reader.readAsDataURL(要读取的文件);

3.监控文件是否读取完成
reader.onload = function () {
  // 读取的文件内容
  reader.result	
};
```

#### 样例-上传图片及时预览

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
  	<!-- 支持多文件 -->
	<input type="file" id="file" multiple>
	<div id="container"></div>
	<script type="text/javascript">
		var file = document.getElementById('file');
		var container = document.getElementById('container');
	    // 用户选择文件确定时触发文件框的 change 事件 
		file.onchange = function () {
			// 获取文件, 文件选择框的 files 属性存贮用户选择的所有文件, 为伪数组类型
			var file = this.files;
			// 循环获取到的图片文件
			for (var i = 0; i < file.length; i++) {
				// 创建文件读取对象 
				var reader = new FileReader();
				// 读取图片文件
				reader.readAsDataURL(file[i]);
				// 文件读取完成
				reader.onload = function () {
					var img = document.createElement('img');
					// 将读取的 base64格式的图片文件
					// this 上下文对象每次改变都会动态的改变自身的值
					img.src = this.result;
					container.appendChild(img);
				}
                
                
                  // 写法2: 闭包写法
                  (function (reader) {
                      reader.onload = function () {
                          var img = document.createElement('img'); 
                          // 将读取的 base64格式的图片文件 
                          img.src = reader.result;
                          // img.src = this.result;
                          container.appendChild(img);
                      }
                  })(reader);
                  // 写法2: 闭包写法
              
			}
		};
	</script>
</body>
</html>
```

### 本地存储

本质：存储数据，以便在需要时获取。类似变量，只不过变量存储在内存中，本地存储存储在硬盘中。

- 方法
  - setItem(key, value)  设置/修改存储内容
  - getItem(key)             获取本地存储中指定的数据 如果数据不存在 返回null
  - removeItem(key)     删除键为 key 的存储内容
  - clear()                        清空本域名下所有存储内容
- window.localStorage
  - 永久生效，除非手动删除（服务器方式访问然后清除缓存）
  - 同一个浏览器且同一个域名下可以多窗口（页面）共享
- window.sessionStorage
  - 生命周期为关闭浏览器窗口
  - 在同一个窗口(页面)下数据可以共享
- 特性
  - 跟 cookie 操作相比较, 本地存储的操作比较方便
  - 容量较大，sessionStorage约5M、localStorage约20M
  - 只能存储字符串类型数据(存贮其他类型的数据会调用 String 方法将其转换为字符串)，可以将对象/数组使用 JSON.stringify() 转换为字符串后再存储
  - 不同的浏览器存储的数据不能实现共享
  - 跟 cookie 相比, 本地存储中存储的数据不会随着请求而进行传输

### 历史管理

单页面web应用简介: 顾名思义有且只有一个页面, 所有的内容和行为都发生在同一个页面中, 大都使用 ajax 动态获取页面然后渲染

优点: 切换页面速度快

缺点: 不产生历史记录(不利于SEO), 打开时(初次加载)比较慢

> history对象，历史记录管理对象。
> 常可用于单页面web应用 SPA (Single Page Application)，为应用添加历史记录。

- history.pushState(data, title, [url] ) 追加一条历史记录  
  - data 用于存储自定义数据
  - title  网页标题，基本上没有被支持，一般设为 '' 空字符串
  - url    可选数据: 以当前域为基础增加一条历史记录, 改变 url 但是不会发送请求(有利于seo)
- history.state 获取最新一条历史记录里面存储的 data 值, 没有则返回 null
- window.onpopstate 事件，当点击历史记录前进按钮或后退按钮时触发 , 只有 window 才能触发此事件
  - 该事件的事件参数对象 e 有一个属性 state 可以获取当前历史记录上存贮的自定义数据 data, 根据 e.state 来判断前进和后退的历史记录, 做出相应的动作

#### 样例:

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<a class="links" data-url="home" href="javascript:;">首页</a>
	<a class="links" data-url="list" href="javascript:;">列表页</a>
	<div id="container"></div>
	<script type="text/javascript" src="js/jquery.min.js"></script>
	<script type="text/javascript">
		var links = $('.links');
		var container = $('#container');
		links.on('click', function () {
			var url = $(this).data('url');
			// 获取最新一条历史记录
			if (url != history.state) {
				// 向浏览器的历史状态中添加一条记录
				history.pushState(url, '', url + '.html');
			}
			if (url === 'home') {
				// 获取首页的数据
				$.ajax({
					url: 'tpl/home.html',
					type: 'get',
					success: function (data) {
						container.html(data);
					}
				});
			}else if (url === 'list') {
				// 获取列表页的数据
				// 获取首页的数据
				$.ajax({
					url: 'tpl/list.html',
					type: 'get',
					success: function (data) {
						container.html(data);
					}
				});
			}
		});
		// 当前进后退按钮被点击时
		window.onpopstate = function (e) {
			// 获取当前历史记录的附加数据 如果没有数据 返回 null
			// 如果附加数据不为空 就去加载页面
			if (e.state !== null) {
				$.ajax({
					url: 'tpl/'+ e.state +'.html',
					type: 'get',
					success: function (data) {
						container.html(data);
					}
				});
			}
		};
	</script>
</body>
</html>
```

### 元素拖放

> HTML5中提供的用于拖拽元素的API。
>
> 被拖拽元素需要设置行内属性 draggable="true" 。

- 被拖拽元素事件
  - dragstart 开始拖拽元素时触发
  - drag 正在拖拽中持续触发
  - dragend 结束拖拽时触发
- 被拖入元素事件
  - dragenter 被拖拽元素上的鼠标进入被拖入元素时触发
  - dragover   被拖拽元素在被拖入元素范围内移动时持续触发
  - dragleave 被拖拽元素上的鼠标离开被拖入元素时触发
    - **dragover 事件的默认行为没被阻止时, 在被拖入元素元素上松开鼠标也会触发此事件**
  - drop 目标拖拽元素在被拖入元素中松开鼠标时触发
    - **如果想要使用 drop 事件, 就需要阻止 dragover 事件的默认行为**

#### 样例-把元素拖进另一个元素

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
		#box1 {
			width: 100px;
			height: 100px;
			background: red;
			position: absolute;
			left: 100px;
			top: 100px;
		}

		#box2 {
			width: 300px;
			height: 300px;
			background: skyblue;
			position: absolute;
			left: 400px;
			top: 100px;
		}
	</style>
</head>
<body>
	<div id="box1" draggable="true"></div>
	<div id="box2"></div>
	<script type="text/javascript">
		var box1 = document.getElementById('box1');
		var box2 = document.getElementById('box2');
		box1.ondragstart = function () {
			box1.style.background = '#000';
		};
		box1.ondragend = function () {
			box1.style.background = 'red';
		};
		box2.ondragover = function (e) {
          	 // 阻止 dragover 事件的默认行为
			e.preventDefault(); // 或者 return false;
		};
		// 如果想要使用ondrop事件 需要阻止ondragover事件的默认行为
		box2.ondrop = function () {
			box2.appendChild(box1);
		};
	</script>
</body>
</html>
```

### 离线应用

> HTML5中我们可以轻松的构建一个离线（无网络状态）应用，只需要创建一个cache manifest文件。

- 优势

  - 1、可配置需要缓存的资源
  - 2、网络无连接应用仍可用
  - 3、本地读取缓存资源，提升访问速度，增强用户体验
  - 4、减少请求，缓解服务器负担

- 缓存清单

  - 一个普通文本文件，其中列出了浏览器应缓存以供离线访问的资源，推荐使用.appcache为后缀名
  - 例如: 我们创建了一个名为 demo.appcache 的文件，然后在需要应用缓存的页面的根元素(html)添加属性manifest="demo.appcache"，路径要保证正确。

- manifest文件格式

  - 1、顶行写 CACHE MANIFEST
  - 2、CACHE: 换行 指定我们需要缓存的静态资源，如.css、image、js等
  - 3、NETWORK: 换行 指定需要在线访问的资源，可使用通配符
  - 4、FALLBACK: 换行 当被缓存的文件找不到时的备用资源

- 其它

  - CACHE: 可以省略，这种情况下将需要缓存的资源写在CACHE MANIFEST
  - 可以指定多个CACHE: NETWORK: FALLBACK:，无顺序限制
  - `#`井号表示单行注释
  - 只有当demo.appcache文件内容发生改变时或者手动清除缓存后，才会重新缓存
  - chrome 可以通过chrome://appcache-internals/工具和离线（offline）模式来调试管理应用缓存

#### 样例文件 demo.appcache

```html
CACHE MANIFEST

# 以下是需要被缓存的文件
CACHE:
images/img1.jpg
images/img2.jpg
images/img3.jpg
images/img4.jpg
images/img5.jpg

# 以下文件需要联网才能访问
NETWORK:
js/index.js

# 当某个资源访问不到时 使用替代文件
FALLBACK:
css/online.css css/offline.css
```

### 网络状态

- 通过 window.navigator.onLine 检测用户当前的网络状况，返回一个布尔值。true 为联网, false
- **在页面首次加载时不会检查网络状况, 所以无法触发以下两个事件, 只有在页面运行时, 才会监听这两个事件**
- window.online 用户网络连接时被调用
- window.offline 用户网络断开时被调用

chrome 的开发者模式下 (F12) Network 选项下有 Offline 选项 和 下拉框, 可以模拟离线/在线模式

**注意: 没有网络连接时, chrome 模拟不了离线/在线模式**

#### 样例

```html
<script type="text/javascript">
  // 当链接网络的时候触发
  window.ononline = function () {
    alert('网络已连接');
    alert(window.navigator.onLine);
  };
  // 当连接断开的时候触发
  window.onoffline = function () {
    alert('网络已断开');
    // 检测当前是否具备网络
    alert(window.navigator.onLine);
  };
</script>
```

### webworker

**本地打开文件不能运行**

提供一个新的进程, 不会阻塞js主进程的运行, 一般将大量计算的任务丢入worker进程中运行, 然后再将结果返回给js主进程

#### 样例

```html
<!-- index.html -->
<!-- 显示worker返回的信息 -->
<div id="msg"></div>
<script>
  window.onload = function () {
    // 创建worker实例对象, 并传入要执行文件的url
    var worker = new Worker('./worker.js');
    // 监听message事件接收返回的信息
    worker.onmessage = function (e) {
      msg.innerHTML += e.data + '<br />';
    }
  }
</script>

<!-- worker.js -->
<script>
  function myCount() {
    for (var i = 0, sum = 0; i < 1000; i++) {
      for (var j = 0; j < 1000; j++) {
        for (var r = 0; r < 1000; r++) {
          sum += i + j + r;
        }
      }
    }
    // 向主线程返回数据
    postMessage(sum);
  }
  // 返回开始时间
  postMessage('start:' + Date.now());
  // 执行函数
  myCount();
  // 返回结束时间
  postMessage('end:' + Date.now());
</script>
```

