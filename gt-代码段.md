## 添加删除类名

```javascript
var tag = document.querySelectorAll(元素);
var arr = tag.className.split(' ');
var index = 0;
if ((index = arr.indexOf(操作的类名)) !== -1) {
  arr.splice(index, 1);
  tag.className = arr.join(' ');
} else {
  arr.push(操作的类名);
  tag.className = arr.join(' ');
}
```

## 实现 insertAfter 函数

```javascript
function insertAfter(node, newNode) {
  var currNode = node.parentNode.lastChild;
  //解决最后一个节点是文本节点的情况
  while (currNode.nodeType !== 1) {
    currNode = currNode.previousSibling;
  }
  if (currNode == node) {
    node.parentNode.appendChild(newNode);
  } else {
    //解决当前节点的下一个兄弟节点是文本节点的情况
    while (node.nextSibling.nodeType !== 1) {
      node = node.nextSibling;
    }
    node.parentNode.insertBefore(newNode, node.nextSibling);
  }
}
```

## 实现事件的追加

```javascript
function myAddEvent(ele, eventType, fn) {
  var oldEvent = ele['on' + eventType];
  //判断当前事件是否已经绑定事件
  ele['on' + eventType] = typeof oldEvent === 'function' ? function () {
    oldEvent();
    fn();
  } : function () {
    fn();
  };
}
```

## 深拷贝

```javascript
function deepCopy(parent, child) {
  for (var key in parent) {
    if (child[key]) {
      continue;
    }
    //细节先判断数组在判断对象,数组也是对象的一种,反向容易把数组创建成对象
    if (parent[key] instanceof Array) {
      child[key] = [];
      deepCopy(parent[key], child[key]);
    } else if (parent[key] instanceof Function) {
      //对于函数可以直接共享,并不影响功能;
      child[key] = parent[key];
    } else if (parent[key] instanceof Object) {
      child[key] = {};
      deepCopy(parent[key], child[key]);
    } else {
      child[key] = parent[key];
    }
  }
}
// 测试
var obj = {
  name: 'aaa',
  cars: ['保时泰', '玛莎拉泰'],
  dog: {
    name: 'mimi',
    age: 10,
  },
  eat: function () {
    console.log('eat');
  }
}
var newObj = {
  name: 'bbb'
}
deepCopy(obj, newObj);
console.dir(newObj);
```

## 带回调函数的dom元素遍历

```javascript
function dom(node, callback) {
  var child = node.children;
  for (var i = 0; i < child.length; i++) {
    callback(child[i]);
    dom(child[i]);
  }
}
// 测试
var ul = document.querySelector('ul');
dom(ul, function (child) {
  child.onclick = function () {
    console.log(this.innerHTML);
  }
})
```

## 观察者模式(订阅-发布模型)

```javascript
function Aim() {
  this.looks = [];
}
Aim.prototype = {
  constructor: Aim,
  //添加观察者
  addLooker: function (fn) {
    this.looks.push(fn);
    return this;
  },
  //删除观察者
  removeLooker: function (fn) {
    this.looks = this.looks.filter(function (item) {
      if (item !== fn) {
        return item;
      }
    });
    return this;
  },
  //同步发布数据
  releave: function (data, content) {
    this.looks.forEach(function (item) {
      item.call(content, data);
    });
    return this;
  }
}

//测试
var aim = new Aim();
//创建两个构造函数,都有render方法
function A() {
  this.render = function (data) {
    console.log('A' + data);
  }
}

function B() {
  this.render = function (data) {
    console.log('B' + data);
  }
}
var a = new A();
var b = new B();
//可链式调用
aim.addLooker(a.render)
   .addLooker(b.render)
   .releave('test');
```

### 简易版

```js
function myEvent() {
  this.callbacks = {}
}
// 订阅事件函数
myEvent.prototype.on = function(eveName, fn) {
  if (!this.callbacks[eveName]) {
    this.calllbacks[eveName] = []
  } 
  // say: [fn1, fn2]
  this.calllbacks[eveName].push(fn)
}
// 发布事件函数
myEvent.prototype.emit = function(eveName) {
  if (!this.callbacks[eveName]) return
  // 遍历触发事件
  this.callbacks.forEach(fn => fn())
}

// == 演示 ==  
let test = new myEvent()
// 订阅事件
test.on('say', () => {
  console.log(1)
})
// 订阅事件
test.on('say', () => {
  console.log(2)
})
// 发布事件
test.emit('say')
```



## 一行评级组件

```javascript
// n为多少星
function getStars(n) {
  var stars = '★★★★★☆☆☆☆☆'.slice(5 - n, 10 - n);
  console.log(stars);
}
// 测试
getStars(0);
getStars(1);
getStars(2);
getStars(3);
getStars(4);
getStars(5);
```



## 数组去重(filter)

```javascript
function unique(arr) {
  if (!Array.isArray(arr)) {
    return new Error('参数错误! 请传入数组.');
  }
  // filter : 过滤数组
  // 回调函数 返回 返回值为 true 的当前值 组成的新数组
  return [].filter.call(arr, function (v, i) {
    // 判断当前值的位置与第一次值在数组中出现的位置是否一致
    // 一致则为不重复值
    return arr.indexOf(v) === i;
  })
}
// 测试
unique([1,1,1,2,3,3,2,2,1]);
```

