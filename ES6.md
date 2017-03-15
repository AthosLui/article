> 对ES6的部分知识点的简要概述与分析  
[查看其他文章](https://github.com/hangyangws/myArticles#文章列表)

# 简谈Promise

> 写在前面:  
在Promise之前，实现异步可使用回调，也可以自己实现类似Promise的结构，比如jQuery的ajax  
回调是很好得解决方案，不过“嵌套多了”就看得人心烦，代码难以阅读  
Promises并非解决具体问题的算法，而已代码组织更好的模式  

先给出一个列子，说明Promise的简单用法

```javascript
function imageLoad(_url) {
    return new Promise(function(resolve, reject) {
        var _image = new _Image(); // 新建Image对象
        _image.onload = function() { // 定义Image对象的加载事件
            resolve('加载成功'); // 如果图片加载成功调用resolve方法
        };
        _image.onerror = function() {
            reject(new Error('加载失败'));
        };
        _image.src = _url;
    });
}

imageLoad() // 执行imageLoad方法，会返回一个Promise实例
    .then( // 注册Promise的回调时间
        _success => console.log(_success), // 加载成功调用的方法
        _error => console.log(_error) // 加载失败调用的方法
    );

```

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
