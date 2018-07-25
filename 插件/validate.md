# validate

## 简介

jQuery Validate 插件为表单提供了强大的验证功能，让客户端表单验证变得更简单，同时提供了大量的定制选项，满足应用程序各种需求。该插件捆绑了一套有用的验证方法，包括 URL 和电子邮件验证，同时提供了一个用来编写用户自定义方法的 API。所有的捆绑方法默认使用英语作为错误信息，且已翻译成其他 37 种语言。

菜鸟教程 validate 插件详细使用 http://www.runoob.com/jquery/jquery-plugin-validate.html

## 简单使用

导入 js 库（使用菜鸟教程提供的CDN）

```html
<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/lib/jquery.js"></script>
<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/dist/jquery.validate.min.js"></script>
<!-- 导入中文提示文件 -->
<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/dist/localization/messages_zh.js"></script>
```

初始化

```html
<script>
  $().ready(function() {
      // 表单元素调用验证函数, 使用默认验证规则
      $("form").validate();
  });
</script>
```

## 样例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		
		input {
			outline: none;
		}

		.error {
			border: 1px solid red;
		}

		.success {
			border: 1px solid green;
		}
	</style>
</head>
<body>
	<form action="">
		<ul>
			<li>
				姓名: 
                 <!-- 
					data-required: 该项必须被填写
                      data-pattern: 该项验证规则
                      data-description: 错误描述规则
                      data-describedby: 绑定错误信息显示的位置
				-->
				<input type="text" data-required data-pattern="^[a-z]{6}$" data-description="a" data-describedby="aa"  name="username">
				<!-- 错误信息显示的位置 -->
				<span id="aa"></span>
			</li>

			<li>
				密码: 
				<input type="password" class="pass" data-description="b" data-describedby="bb" data-required data-pattern="^\d{6}$" name="pass">
				<span id="bb"></span>
			</li>


			<li>
				确认密码: 
				<input type="password" data-description="c" data-conditional="ee" data-required data-pattern="^\d{6}$" name="pass" data-describedby="cc">
				<span id="cc"></span>
			</li>


			<li><input type="submit" value="提交"></li>
		</ul>
	</form>
	<script src="./libs/jquery.js"></script>
	<script src='./libs/jquery-validate.js'></script>
	<script>
		// 1. 调用方法
		$('form').validate({
          
			// 值为 false 时，表示使用 ajax 进行表单提交
			sendForm: false,

			// 在输入时进行验证
			onKeyup: true,

			// 整个表单合法时，会执行回调
			valid: function () {
				console.log('所表表单项都合法')
				console.log('可以使用 ajax 提交了');

				// $.ajax({
				// 	url: '',
				// 	data: ''
				// })
			},

			// 只要有一个不合法的表单项，都会执行此回调
			eachInvalidField: function () {
				console.log('只要有不合法的表单项，就会执行');
				console.log('可能会执行多次');

				// 这个回调下的 this 指向不合法的那个元素
				console.log(this);

				// $(this).toggleClass('success error');
				$(this).addClass('error').removeClass('success');

			},

			eachValidField: function () {
				console.log('只要有合法的表单项，就会执行');
				console.log('可能会执行多次');

				// 这个回调下的 this 指向指向合法的那个元素
				console.log(this);

				$(this).addClass('success').removeClass('error');
			},

			// 自定义验证条件
			// 比正则表达式更具体
			// 例如 确认密码
			// 例如 年龄不能超过多少岁
			conditional: {
				ee: function (val) {
					// console.log(val);
					

					// if(val == document.querySelector('.pass').value) {
					// 	return true;
					// }

					// 
					return val == document.querySelector('.pass').value;

					// 表示合法
					// return true;
					// 表示不合法
					// return false;
				}
			},

			// 错误信息提示
			// 需要为不同的表单指定 data-description
			// 才可以实现不同的表单提示不同的错误信息
			description: {
				a: {
					required: '姓名不能为空',
					pattern: '只能为英文字母'
				},
				b: {
					required: '密码不能为空',
					pattern: '密码只能为6位数字'
				},
				c: {
					required: '密码不能为空',
					pattern: '密码只能为6位数字',
					conditional: '两次密码不一致'
				}
			}
		});

		// 2. 需要为验证的元素添加验证规则，通过 html 属性添加
		// a) data-required 必需（填）的
		// b) data-pattern 支持正则表达式

	</script>
</body>
</html>
```