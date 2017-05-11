# Web Worker

### 简介 & 背景

浏览器限制一个网页在一个 `进程` 中执行 -> JS只能在这个进程的一个 `线程` 执行 -> 高负荷的运算 -> 一个线程搞不定  
web worker 可以理解为，`网络的苦力工`，处理繁重的任务、运算，那么 `Web Worker` 就是为了解决 `浏览器性能` 而生  
web worker 运行在线程中，JS也是运行在线程中，线程之间的通信可以使用 `postMessage` 进行双向通信

### 一个乘法 DEMO

[点我](http://hangyangws.win/myDemo/apps/web_worker/)

### 关闭 worker 实例（杀掉线程）

> 官方推荐是，使用 self.close 进行内部的自动关闭，这样能防止, 意外关闭正在运行的 worker

1. workerObj.terminate(): 在外部终结该 worker
1. self.close(): 在 worker 内部自动终结

### 作用域

全局索引就是 self 和 this ，来获取 worker 自带的方法

### 注意事项

worker 引用的就是 js 文件  
由于 worker 是独立的线程，他和 main js threading 有很大区别的

worker **访问权限**有

1. window.navigator 相关属性和方法
1. 只读的 window.location 内容.
1. window.XMLHttpRequest （卧槽… 可以访问这个那就不得了， worker 就可以利用 ajax 来和后台进行通信了）
1. setInterval 相关时间函数

**同域限制**

worker 在访问时, 只能是在同一 host 下才行. 即, 你的 worker 只能处于指定目录下的 path 中  
所以：本地调试 file://xxx 的话, 也不能使用 worker

在当前的 worker 加载其他库文件

可以使用 **importScripts** 来导入（自动缓存文件）  
`importScripts('example1.js','example2.js')`

### 使用场景

根据 worker 独立线程特性，可以把大规模数据并发， I/O 操作都可以交给他  
总的来说有这些场景

- 懒加载数据
- 文本分析
- 流媒体数据处理
- web database 的更新

---

# Service Worker

[Service Worker 入门](https://www.w3ctech.com/topic/866)
[服务工作线程注册](https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/registration)
[Service Worker 全面进阶](http://ivweb.io/topic/5876d4ee441a881744b0d6d6)

### 概述

它使得开发者可以支持非常好的离线体验，给予开发者完全控制离线数据的能力  
service worker 是一段运行在浏览器后台进程里的脚本，它独立于当前页面  
原生 APP 有 Web 通常所不具备的富离线体验、定时的静默更新、消息通知推送……  
而 Service workers 标准让在Web拥有这些功能成为可能

Service workers 由 cache 和 [Worker](https://www.villainhr.com/page/2016/08/22/Web%20Worker)二部分组成  
不会阻碍当前 js 进程的执行，确保性能第一

SW 是基于 HTTPS 的，如果你的网站不是 HTTPS，那么基本上你也别想了 SW  
这估计造成了一个困难，即，我调试 SW 的时候咋办  
解决办法也是有的，使用 charles 或者 fildder 完成域名映射即可

SW 是挂载到 navigator 下的对象

```js
if ('serviceWorker' in navigator) {
  // ....
}
```

### 注意事项

1. 它是 JavaScript Worker ，所以它不能直接操作 DOM ，但是可以通过 postMessage 与页面之间通信，如果需要的话，让页面自己去操作DOM
1. Service worker 是一个可编程的**网络代理**，允许开发者控制页面上处理的网络请求
1. 在不被使用的时候，会自己终止，而当它再次被用到的时候，会被重新激活

  > 所以你不能依赖于 service worker 的 onfecth 和 onmessage 的处理函数中的全局状态  
  如果你想要保存一些持久化的信息，你可以在 service worker 里使用 IndexedDB API

1. service work 会收到他域下的所有fetch事件，所以注册时，要注意路径

### 生命周期

![lifycycle](/img/lifycycle.png)

要让一个 service worker 在你的网站上生效，你需要先在你的网页中注册它  
浏览器会在后台默默启动一个 service worker 的安装过程  
安装过程中，浏览器会加载并缓存一些静态资源，如果**所有**的文件被缓存成功，则安装成功，如果有**任何**文件加载或缓存失败，则安装失败  
失败后会重新尝试

后台进程: SW 就是一个 worker 独立于当前网页进程。  
网络代理: SW 可以用来代理请求，缓存文件  
灵活触发: 需要的时候吊起，不需要的时候睡眠（这个是个坑）  
异步控制: SW 内部使用 promise 来进行控制。

### 开始使用

注册（告诉浏览器你的 service worker 脚本在哪里）  
如果某个 service worker 已经被注册过，再次注册浏览器会自动忽略

```javascript
window.addEventListener('DOMContentLoaded', function() {
  // 执行注册
  navigator.serviceWorker.register('/sw.js').then(function(registration) {

  }).catch(function(err) {

  })
})
```

但浏览器的资源也是有限的，浏览器分配给你网页的内存就这么多，你再开个 SW（这个很大的。。。），容易闪退  
为了减少性能损耗，我们一般直接在 onload 事件里面注册 SW

### 查看

打开 `chrome://inspect/#service-workers` 查看当前浏览器中正在注册的 SW  
`chrome://serviceworker-internals` 用来查看当前浏览器中所有注册好的 SW
