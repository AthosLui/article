> 对ES6的部分知识点的简要概述与分析  
[查看其他文章](https://github.com/hangyangws/myArticles#文章列表)

# 简谈Promise

> 写在前面:  
在Promise之前，实现异步可使用回调，也可以自己实现类似Promise的结构，比如jQuery的ajax  
回调是很好得解决方案，不过“嵌套多了”就看得人心烦，代码难以阅读  
Promises并非解决具体问题的算法，而已代码组织更好的模式

先给出一个列子，说明Promise的简单用法

```javascript
// 注意：为什么要用函数把“new Promise”包起来，因为new Promise时，也会执行函数内部代码
//      所以通常用一个函数把“new Promise”包起来，在函数内部return Promise的实例

function imageLoad(_url) {
    return new Promise(function(resolve, reject) {
        var _image = new Image(); // 新建Image对象
        _image.onload = function() { // 定义Image对象的加载事件
            resolve('加载成功'); // 如果图片加载成功调用resolve方法
        };
        _image.onerror = function() {
            reject(new Error('加载失败'));
        };
        _image.src = _url;
    });
}

imageLoad('https://avatars2.githubusercontent.com/u/9067839') // 执行imageLoad方法，会返回一个Promise实例
    .then( // 注册Promise的回调事件
        _success => console.log(_success), // 加载成功调用的方法
        _error => console.log(_error) // 加载失败时调用的方法（比如当图片地址不存在的时候）
    );

// 仔细观察上面的代码，开发者会发现
// 创建Promise实例时传入函数的第一个参数指向的就是“Promise实例的then方法的第一个参数”
// 同理，
// 创建Promise实例时传入函数的第二个参数指向的就是“Promise实例的then方法的第二个参数”
// 所以，
// resolve执行时等同执行then的第一个函数参数；reject执行时等同执行then的第二个函数参数
```

认真看了上面的典型的简单的Promise例子，开发者应该对Promise不陌生了，至少对then方法不陌生^_^  
下面，我们就开始了解then方法之外的其他方法

Promise的静态方法

- Promise.resolve()
- Promise.reject()
- Promise.all()
- Promise.race()

Promise原型链方法（又称实例方法）

- Promise.prototype.then()
- Promise.prototype.catch()

```javascript
```

> [参考](http://es6.ruanyifeng.com/#docs/promise#Promise-的含义)
[参考2](http://liubin.org/promises-book/#introduction)
[参考3](http://coderlt.coding.me/2016/12/03/promise-in-depth-an-introduction-1/#comments)
