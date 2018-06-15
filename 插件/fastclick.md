# fastclick

## 简介

去除移动端 click 事件 300ms 延迟问题

300ms延迟主要用于判断是否还有第二次点击, 延迟之内点击两次为双击事件

## 使用

```html
<!-- 插件引入 -->
<script src="./libs/fastclick.min.js"></script>
<script>
    // 当页面的dom元素加载完成 
    document.addEventListener('DOMContentLoaded', function() {
        // 初始化方法 
        FastClick.attach(document.body);
    }, false);
    // 正常使用click事件就可以了 
</script>
```

