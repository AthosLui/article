### Web 推送技术

[参考链接](https://www.villainhr.com/page/2017/01/08/Web%20%E6%8E%A8%E9%80%81%E6%8A%80%E6%9C%AF)  
涉及知识点：  

1. Push
1. Notification
1. Service Worker

### Prepack

[prepack 官网](https://prepack.io/)  
[prepack GitHuB repo](https://github.com/facebook/prepack)

官方宣称 Prepack 是一个优化 JavaScript 源代码的工具  
实际上它是一个 JavaScript 的部分求值器（Partial Evaluator）  
可在编译时执行原本在运行时的计算过程，并通过重写 JavaScript 代码来提高其执行效率  
Prepack 用简单的赋值序列来等效替换 JavaScript 代码包中的全局代码  
从而消除了中间计算过程以及对象分配的操作  
对于重初始化的代码，Prepack 可以有效缓存 JavaScript 解析的结果，优化效果最佳

### Others

[Rekit 2.0 构建基于 React+Redux+React-router 的可扩展 Web 应用](https://zhuanlan.zhihu.com/p/27938754)

[你一定要知道的 Chrome DevTool 新功能](http://web.jobbole.com/91769/)
