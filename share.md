# 周五分享暂选清单

### Web推送技术

[参考链接](https://www.villainhr.com/page/2017/01/08/Web%20%E6%8E%A8%E9%80%81%E6%8A%80%E6%9C%AF)  
涉及知识点：  

1. Push
1. Notification
1. Service Worker

### 浏览器端进行图片压缩 && 上传

[参考链接](https://sebastianblade.com/browser-side-image-compress-and-upload/)  
涉及知识点：  

1. URL.createObjectURL()
1. FileReader
1. Canvas

### Service Worker

[参考链接1](https://juejin.im/post/591028fc2f301e006c291c4b)  
[参考链接2](https://segmentfault.com/a/1190000006678016)  
涉及知识点：  

1. web worker
1. Service Worker

### Prepack

[参考链接1](https://prepack.io/)  
[参考链接2](https://github.com/facebook/prepack)  

官方宣称Prepack是一个优化JavaScript源代码的工具  
实际上它是一个JavaScript的部分求值器（Partial Evaluator）  
可在编译时执行原本在运行时的计算过程，并通过重写JavaScript代码来提高其执行效率  
Prepack用简单的赋值序列来等效替换JavaScript代码包中的全局代码  
从而消除了中间计算过程以及对象分配的操作  
对于重初始化的代码，Prepack可以有效缓存JavaScript解析的结果，优化效果最佳
