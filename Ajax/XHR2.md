## 简介



## 请求超时

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', './timeout.php');

// 当请求时间超过 3 秒后，自动停止请求
// 默认单位为毫秒(ms)
xhr.timeout = 3000;
// 通过事件可以监听到超时事件
// 简写为 xhr.ontimeout
xhr.addEventListener('timeout', function () {
  alert('请求超时，请稍后重试');
})

xhr.send();
xhr.addEventListener('readystatechange', function () {
  if(this.readyState === 4 && this.status === 200) {
	console.log(this.responseText);
  }
})
```

## 表单管理

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>表单管理</title>
</head>
<body>
	<form action="">
		<li>
			姓名: <input type="text" name="username">
		</li>
		<li>
			密码: <input type="password" name="pass">
		</li>
		<li>
			性别: 男 <input type="radio" name="gender" value="0">
			      女 <input type="radio" name="gender" value="1">
		</li>
		<li>
			<input type="submit" value="提交">
		</li>
	</form>
	<script>
      	// 获取表单元素
		var form = document.querySelector('form');
      	// 监听表单 submit 事件
		form.addEventListener('submit', function (e) {
			// 通过 ajax 提交表单
			var xhr = new XMLHttpRequest();
			xhr.open('post', 'form.php');
          
			// 通过（H5提供）内置的构造函数 FormData, 可以实现一次性获取所有表单元素的值(文件表单框无法获取), 创建一个 FormData 实例, 将要获取的 form 表单传入即可,
             // 不可以直观的对数据进行查看
			var data = new FormData(form);
			// 将 data 作为参数传递给 send 函数, 后台就可以正常获取传递的表单参数
			xhr.send(data);
          
			xhr.addEventListener('readystatechange', function () {
				if(this.readyState === 4 && this.status === 200) {
             		 console.log(this.responseText);
				}
			})
			// 阻止 submit 提交的默认行为
             // 表单元素的 原生submit 事件不能使用 return false 阻止
			e.preventDefault();	
		})

		// $('form').on('submit', function (e) {
		// 	// 在 jQuery 中事件回调函数中
		// 	// 的 return false = e.preventDefault() + e.stopPropagation()
		// 	return false;
		// })
	</script>
</body>
</html>
```

## 文件上传

+ **xhr1.0 版本不能进行文件上传** 使用 flash 技术实现

### 实例: 单文件上传实现本地图片预览

文件目录结构:   index.html     upfile.php      文件夹 uploads

html代码: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文件上传</title>
</head>
<body>
	<form action="">
		<li>
			姓名: <input type="text" name="username">
		</li>
		<li>
			密码: <input type="password" name="pass">
		</li>
		<li>头像: <input type="file" name="avatar" class="upfile"></li>
		<li>
			性别: 男 <input type="radio" name="gender" value="0">
			      女 <input type="radio" name="gender" value="1">
		</li>
		<li>
			<input type="submit" value="提交">
		</li>
	</form>
	<img src="" alt="图片">
	<script>
		var file = document.querySelector('.upfile');
         // 用户选择文件后, 会触发文件表单域的 change 事件
		file.addEventListener('change', function () {
			var xhr = new XMLHttpRequest();
			xhr.open('post', 'upfile.php');
          
			// 创建一个空的 FormData 实例, 通过实例对数据进行处理
			var data = new FormData();
			// data 通过自带的 append 方法(不同于jQuery的 append 方法)，可以追加数据
          	 // 将用户选择的文件追加到 data 中, 键名应与文件表单域 name 相同
          	 // 文件表单域的 files 属性存储的用户选择的文件, 其值为伪数组
			data.append('avatar', this.files[0]);
             // 将包含文件的 data 数据发送给后台 
			xhr.send(data);
          
			xhr.addEventListener('readystatechange', function () {
				if(this.readyState === 4 && this.status == 200) {
                  	  // 设置图片的 src 属性
					document.querySelector('img').src = this.responseText;
				}
			})
		})


	</script>
</body>
</html>
```

php代码:

```php
<?php
	// 通过系统函数 pathinfo 可以获取文件的后缀
	// 获取文件后缀名
	$ext = pathinfo($_FILES['avatar']['name'])['extension'];	
	// 使用 时间戳 创建文件名
	// 拼接文件存贮路径
	$path = './uploads/' . time() . '.' . $ext;
	// 转移临时文件到指定存贮目录
	move_uploaded_file($_FILES['avatar']['tmp_name'], $path);
	// 返回文件存贮路径
	echo $path;
```

## 文件上传进度

+ **xhr1.0 版本不能原生支持文件上传进度显示** 使用 flash 技术实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>上传进度</title>
	<style>
		.progress {
			width: 300px;
			height: 15px;
			background-color: pink;
		}

		.loaded {
			width: 0;
			height: 15px;
			background-color: green;
		}
	</style>
</head>
<body>
    <form action="">
		<input type="file" class="upfile" name="avatar">
    </form>
  	<!-- 总进度条 -->
	<div class="progress">
      	 <!-- 上传进度条 -->
		<div class="loaded"></div>
	</div>
	<script>
		var file = document.querySelector('.upfile');
		file.addEventListener('change', function () {
			var xhr = new XMLHttpRequest();
			xhr.open('post', './upload.php');

			// 在send方法调用前，对上传进度进行监听
			// 事件名称为 progress, 为多次触发事件, 每隔一段时间触发一次
			xhr.upload.addEventListener('progress', function (e) {
				// 通过事件对象，可以获得上传文件的具体信息（上传进度）
				// console.log(e);

				// e.loaded 为当前上传的大小
				// e.total 文件总大小
				var percent = e.loaded / e.total;
				// 转成百分制
				percent = percent * 100 + '%';
              	 // 将上传进度条的宽度设置为百分比
				document.querySelector('.loaded').style.width = percent;
			})

			// 通过 FormData 对上传文件数据进行处理
			var data = new FormData();
			data.append('avatar', this.files[0]);
			xhr.send(data);
			xhr.addEventListener('readystatechange', function () {
				if(this.readyState === 4 && this.status === 200) {
					console.log(this.responseText);
				}
			})
		})
	</script>
</body>
</html>
```

## 新增事件api

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>事件处理</title>
</head>
<body>
	<button>按钮</button>
	<script>
		var btn = document.querySelector('button');
		btn.addEventListener('click', function () {
			var xhr = new XMLHttpRequest();
			xhr.open('get', './timeout.php');
          
			// loadstart 请求开始时触发, 需要写在 send 方法前
			xhr.addEventListener('loadstart', function () {
				console.log('请求开始');
			})
          
			xhr.send();

			// readyState 为 4 触发 load 事件
			xhr.addEventListener('load', function () {
              	 // 处理响应数据
				console.log(this.responseText);
			})

			// loadend 请求结束时触发
			xhr.addEventListener('loadend', function () {
				console.log('请求结束');
			})

			// 当网络发生固障，触发 error 事件
			xhr.addEventListener('error', function () {
				console.log('网络出现了问题');
			})
		})
	</script>
</body>
</html>
```

