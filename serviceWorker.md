# Web Worker

[link-Web Worker](https://www.villainhr.com/page/2016/08/22/Web%20Worker)

# Service Worker

[Service Worker 入门](https://www.w3ctech.com/topic/866)
[link-服务工作线程注册](https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/registration)
[link-ervice Worker](https://juejin.im/post/591028fc2f301e006c291c4b)

### 概述

由cache和[Worker](https://www.villainhr.com/page/2016/08/22/Web%20Worker)二部分组成  
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

### 生命周期

![lifycycle](/img/lifycycle.png)

后台进程: SW 就是一个 worker 独立于当前网页进程。  
网络代理: SW 可以用来代理请求，缓存文件  
灵活触发: 需要的时候吊起，不需要的时候睡眠（这个是个坑）  
异步控制: SW 内部使用 promise 来进行控制。


### 注册

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





