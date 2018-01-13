# fetch

> fetch 提供一个获取资源的接口(包括跨网络)  
fetch 可看做 ES6 对 `XMLHttpRequest` 的升级方法  

fetch 请求默认不带 cookie ，需设置 fetch(url, {credentials: 'include'})  
当服务器返回`400、500`状态码时并不会 reject  
只有网络错误这些导致请求不能完成时， fetch 才会被 reject

# import

# super

[link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)

# class

[link](https://github.com/ruanyf/es6tutorial/blob/a5ed53c5399c14cfaea4ca7e97957b999fba4807/docs/class.md)  
[link](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)  
[link](http://es6.ruanyifeng.com/#docs/class#Class 基本语法)

ES6 明确规定， Class 内部只有静态方法，没有静态属性  
ES7 有一个静态属性的提案，目前 Babel 转码器支持

```JS
class Foo {}

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

# rest 参数

> rest 参数，形式为「...变量名」，用于获取函数多余参数

## 一个 Demo

```javascript
const restFunction = (...rest) => {
  console.log(rest)
}

restFunction(1, 2)
// 打印：[1, 2]
```

## 注意

1. rest 参数只能放在形参的最后一位
1. 箭头函数中，单个 rest 参数不能省略小括号

比如：

```javascript
const restFunction = (...rest, nextParam) => {}
// 报错：Rest parameter must be last formal parameter

const restFunction = ...rest => {}
// 报错：Unexpected token ...
```

# 扩展运算符「spread」

扩展运算符，看起来和 rest 参数外观相似，也是「...」，  
不过和 rest 参数功能可是不一样呢

扩展运算符将可 iterator 对象遍历为「逗号分隔的参数序列」
