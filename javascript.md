[查看其他文章](https://github.com/hangyangws/myArticles#articles-list)

# javascript

### 数据类型
> 6种原始类型、引用类型  
> 记住没有数组（array）类型

- 原始类型（特点：不可变“除非重置当前变量，否则不能改变变量值”）
    1. Null(只有一个值： null)
    1. Undefined(一个没有被赋值的变量会有个默认值 undefined)
    1. Number
    1. Boolean(两个值：true 和 false)
    1. String
    1. [Symbol](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)（ES6新增）
- Object(对象指内存中的可以被标识符引用的一块区域，数组、对象…)

### 数据类型检测之`typeof`

typeof(对变量或值调用 typeof 运算符将返回(字符串)下列值之一)

1. undefined - Undefined类型
1. number - Number类型
1. boolean - Boolean类型
1. string - String类型
1. symbol - Symbol类型(ECMAScript6新增)
1. function - 函数对象([[Call]]在ECMA-262条款中实现了)
1. object - 引用类型 或 Null类型

```javascript
typeof Function // function (Function是函数对象)
typeof new Function // function (new Function也是是函数对象，同等：var func = function(){})
typeof new new Function // object (new Function也是是“构造函数（类）”，new new Function就是“实例（对象）”)
typeof Array // function (Array是函数对象)
typeof new Array // object（实例化的Array就是object）
```

### 变量赋值时候的返回值
> 定义变量的时候赋值返回:undefined  
> 给已声明变量赋值时候返回当前赋值

```javascript
var name = 'hangyang'; // 返回：undefined
name = 'ws'; // 返回：ws
```

### defer && async
> 现在很多开发者包括我都喜欢把JS文件放在body闭合标签之前，这是问什么呢？  
> 因为加载`<script src="xxx.js">`会堵塞`DOM`树的解析与构建  
> 解析到`<script src="xxx.js">`时，浏览器会下载当前JS文件，这段时间`DOM`树的构建是停止的  
> 如果`<script src="xxx.js">`下载需要6秒，并且放在`<head>`里面，那么页面会延迟6面加载，出现6秒**白屏**

- defer（翻译：推迟）

    使用方式：  
    添加`defer`属性：`<script src="xxx.js" defer>`  
    作用效果：  
    当浏览器解析到`<script>`时，同时（异步）解析`DOM`，并且开始下载`JS`  
    当`JS`下载完成后，并不会马上执行  
    而是继续解析`DOM`，当`DOM`构建完成(DOMContentLoaded)后再执行`JS`内容
- async（翻译：异步）

    使用方式：  
    添加`async`属性：`<script src="xxx.js" async>`  
    作用效果：  
    当浏览器解析到`<script>`时，同时（异步）解析`DOM`，并且开始下载`JS`  
    当`JS`下载完成后，就会马上执行，并且停止`DOM`的解析  
    当`JS`执行完成后，又开始解析`DOM`
- 总结

    `defer`和`async`在下载`JS`时是一样的，相较`DOM`解析都是异步  
    它俩的差别在于`JS`下载完之后何时执行  
    `defer`执行顺序是和脚本放置位置一样  
    `async`执行则是乱序，不管脚本放置顺序如何，只要加载完了就会立刻执行  
    `defer`最接近**把脚本放在`<body>`闭合标签前**的效果  
    `async`用到的场景比较少

### 元素视图之getBoundingClientRect()、getClientRects()、elementFromPoint()
- getBoundingClientRect

    > 用于判断元素尺寸和位置

    - 用法：`element.getBoundingClientRect()`
    - 返回值：
    ```javascript
    {
        // 下面的值除了width、height外都可能为负数（元素不在视图内的时候）
        // 以下值，都是number类型
        // 注意：IE7以下浏览器，视口的左边默认是(2, 2)，开发者注意
        top: 0, // 元素上border相对于视口上边的纵坐标
        bottom: 0, // 元素下border相对于视口上边的纵坐标
        left: 0, // 元素左border相对视口左边的横坐标
        right: 0, // 元素右border相对视口左边的横坐标
        width: 0, // 元素宽度（border+padding+width）
        height: 0 // 元素高度（border+padding+width）
    }
    ```
- getClientRects

- elementFromPoint

### arguments、callee、caller
```javascript
```

### call、bind、apply
```javascript
```

### 函数（类）的继承与重载
- 继承
    ```javascript
    // js可以使用对象冒充实现继承的（平时少用）
    function Father(name, age) {
        // 代码A(承上)
        this.name = name;
        this.age = age;
        this.show = function() {
            console.log(this.name, this.age);
        }
        // 代码B(启下)
    }

    function Son(name, age) {
        this.Father = Father; // Son内部的Father属性指向Father函数（类）
        this.Father(name, age); // 执行Son内部的Father函数，等同于吧代码A和代码B之间的代码执行了一遍，因而实现“继承”
    }
    var me = new Son('hangyangws', 21);
    me.name; // hangyangws
    me.show(); // hangyangws 21
    ```
- 重载
    > js从常理来说是不支持重载的，但是又可以说是天然支持重载，因为js天然支持可变参数，而且我们在函数内部可以通过arguments对象的length属性，而做出相应的处理
    > 目前[函数式编程](http://baike.baidu.com/link?url=K_XE6rft1YiCQ9tMPac33DgqW_wdyd6WhjhKR37AbEMCp_Avfnb2oojydKBq4WqrqTSNy9Hjo0giLsK5SO95Top5QUQj0ZVC5ZM4nSK-mysX2qOvoGyFr-Ua2Ne7VAEEdCLId79H_9TkbfqdZFbya_)比较火，所以“重载”已经不再兴起

    ```javascript
    // 重载简单示范
    function argumentsTest() {
        var _paraLenth = arguments.length;
        switch(_paraLenth) {
            case 0:
                // 0个参数时，函数做什么…
                ;break;
            case 1:
                // 1个参数时，函数做什么…
                ;break;
            default:
                // 其他参数个数时，函数做什么…
                ;
        }
    }
    ```

### promise及原理

### fetch

### 位运算符
> & |

### 闭包
> 闭包实际上设计一个对象的属性，何时被gc处理的问题 闭包和gc是相关联的

```javascript
```

### 数组相关
- length

    ```javascript
    // 数组的长度是根据下标的最大而确定的
    var arr = new Array();
    arr['one'] = 'one';
    arr['two'] = 'two';
    arr.length; // 返回：0
    arr[100] = 100;
    arr.length; // 返回：101

    // 手动赋值数组长度可以删减多余元素
    var arr = [1, 2, 3, 4];
    arr.length = 2;
    console.log(arr); // [1, 2]
    ```