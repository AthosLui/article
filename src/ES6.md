# Generator

> [阮老师 ES6入门](http://es6.ruanyifeng.com/#docs/generator)

# fetch

> fetch 提供一个获取资源的接口(包括跨网络)
fetch 可看做 ES6对`XMLHttpRequest`的升级方法  

fetch 请求默认不带 cookie ，需设置 fetch(url, {credentials: 'include'})  
当服务器返回`400、500`状态码时并不会 reject  
只有网络错误这些导致请求不能完成时， fetch 才会被 reject

### import

### super

[link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)

### class

[link](https://github.com/ruanyf/es6tutorial/blob/a5ed53c5399c14cfaea4ca7e97957b999fba4807/docs/class.md)  
[link](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)  
[link](http://es6.ruanyifeng.com/#docs/class#Class 基本语法)

ES6 明确规定， Class 内部只有静态方法，没有静态属性  
ES7 有一个静态属性的提案，目前 Babel 转码器支持

```JS
class Foo {
}

Foo.prop = 1
Foo.prop // 1
//上面的写法为 Foo 类定义了一个静态属性 prop

// 以下两种写法都无效
class Foo {
  // 写法一
  prop: 2

  // 写法二
  static prop: 2
}

Foo.prop // undefined
```
