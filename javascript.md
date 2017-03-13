> JavaScript相关知识  
[查看其他文章](https://github.com/hangyangws/myArticles#文章列表)

# JS的7种数据类型

### 6种原始类型

> 原始类型特点：不可变  
除非重置当前变量，否则不能改变变量值

1. **Null** (只有一个值： null)
1. **Undefined** (一个没有被赋值的变量会有个默认值undefined)
1. **Number**
1. **Boolean** (只有两个值：true 和 false)
1. **String**
1. [**Symbol**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol) （ES6新增）

### 1种引用类型

> 对象指内存中的可以被标识符引用的一块区域  
比如：数组、对象…

1. **Object**

# 数据类型检测之`typeof`

typeof(对变量或值调用 typeof 运算符将返回(字符串)下列值之一)

1. **undefined** (Undefined类型)
1. **number** (Number类型)
1. **boolean** (Boolean类型)
1. **string** (String类型)
1. **symbol** (Symbol类型 - ECMAScript6新增)
1. **function** (函数对象 - ECMA-262条款中实现了)
1. **object** (引用类型 或 Null类型)

上面的返回值中的前5种都好理解，但是后2种：什么时候返回object，什么时候返回function  
请看列子与解释：

```javascript
typeof Function // 返回：function (Function是函数对象)

typeof new Function // 返回：function (new Function是函数对象)

var func = function(){};
typeof func // 返回：function (func是函数对象，和上一个列子一样的意思)

typeof new new Function // 返回：object (第一次new返回函数对象，第二次new返回实例“引用类型”)

typeof Array // 返回：function (Array是函数对象)

typeof new Array // 返回：object（实例化的Array是“引用类型”）

typeof [1, 2] // 返回：obejct （[1 ,2]是“引用类型”，和上一个列子一样的意思）

typeof Object // 返回：function（Object是函数对象，你可以理解为浏览器定义了一个函数:"var Object = function() {}"）

typeof {a: 'a'} // 返回：object（{a: 'a'}是“引用类型”）

// 综上所述，开发者要注意了：数组并不是数组，对象并不是对象 ^_^，容我幽默一下
```

# 数据类型检测之`instanceof`

> 语法`object instanceof constructor`  
instanceof通过原型链来判断对象时候属于它的父类型，判断原则：  
先查找object的`__proto__`链，同步查找constructor的`prototype`链，如果两者相等，就返回true

```javascript
function Func() {};
var obj = new Func;
obj instanceof Func; // 返回：true （因为 obj.__proto__ === Func.prototype）

Func.prototype = {}; // 重定向Func的prototype

var  obj2 = new Func;
obj instanceof Func; // 返回：false (因为Func的prototype指向一个空对象，这个空对象不在obj的原型链上)
obj2 instanceof Func; // 返回：true

function Func2() {};
Func2.prototype = new Func();

var obj3 = new Func2();
obj3 instanceof Func; // 返回：true （因为obj3.__proto__.__proto__ === Func.prototype）
obj3 instanceof Func2; // 返回：true （因为obj3.__proto__ === Func2.prototype）
```

# defer和async

> 开发者喜欢把JS文件放在body闭合标签之前，这是问什么呢  
因为加载`<script src="xxx.js">`会堵塞`DOM`树的解析与构建  
解析到`<script src="xxx.js">`时，浏览器会停止`DOM`树的构建，而去下载当前JS文件  
如果`<script src="xxx.js">`下载需要6秒，并且放在`<head>`里面，那么页面会延迟6秒加载，出现6秒白屏

### defer（翻译：推迟）

**使用方式**：  
添加`defer`属性：`<script src="xxx.js" defer>`

**作用效果**：  
当浏览器解析到`<script>`时，同时（异步）解析`DOM`，并且开始下载`JS`  
当`JS`下载完成后，并不会马上执行  
而是继续解析`DOM`，当`DOM`构建完成(DOMContentLoaded)后再执行`JS`内容

### async（翻译：异步）

**使用方式**：  
添加`async`属性：`<script src="xxx.js" async>`

**作用效果**：  
当浏览器解析到`<script>`时，同时（异步）解析`DOM`，并且开始下载`JS`  
当`JS`下载完成后，就会马上执行，并且停止`DOM`的解析  
当`JS`执行完成后，又开始解析`DOM`

### 总结defer、async

`defer`和`async`在下载`JS`时是一样的，相较`DOM`解析都是异步  
它俩的差别在于：`JS`下载完之后何时执行  
`defer`执行顺序是和脚本放置位置一样  
`async`执行则是乱序，不管脚本放置顺序如何，只要加载完了就会立刻执行  
`defer`的效果最接近“**把脚本放在`<body>`闭合标签前**”  
`async`用到的场景比较少

# 元素视图之getBoundingClientRect()、getClientRects()、elementFromPoint()

### getBoundingClientRect

> 用于判断元素尺寸和位置

**用法**：  
`element.getBoundingClientRect()`

**返回值**：

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

### getClientRects  

> 主要用于行内(inline)元素（如：`<a>`…）  
可以用于判断行内元素是否换行，以及行内元素的每一行的位置偏移

**用法**：  
`element.getClientRects()`

**返回值**：
`一个TextRectangle对象（一个类数组对象）`

```javascript
var test = element.getClientRects();
test.length; // 如果element是非inline元素，test.length为1，否则为元素的行数
// test[0]、test[0]…返回的值与getBoundingClientRect类似
```

### elementFromPoint

> 查看视口中指定位置是什么元素  
注意：返回的元素是指定坐标的最上层（z-index最大）和最里层（最里层的子元素）的Element对象

**用法**：
`document.elementFromPoint(x, y)`

**返回值**：
`Element对象`

# 函数继承

> 我们知道，JS不同于C++这类语言，支持继承，但是我们可以“模仿”

```javascript
// 定义一个简单的父类
function Father(name) {
    this.name = name || 'noName';
    this.show = function() {
        console.log(this.name);
    }
}


// 方法一：“原型链”实现继承
function Son1() {}
Son1.prototype = new Father;
// 代码测试
var son1 = new Son1();
son1.show(); // 返回：noName
son1.prototype.name = 'hangyangws';
son1.show(); // 返回：hangyangws
// 分析：（缺点）创建子类实例时，无法向父类构造函数传参
//      （缺点）无法实现多重继承


// 方法二：使用“对象冒充”实现继承（也叫“构造继承”）
function Son2(name) {
    Father.call(this, name);
}
// 上面函数还有另一种写法
function Son2(name) {
    this.Father = Father; // Son内部的Father属性指向Father函数
    this.Father(name); // 执行Son内部的Father函数
}
// 代码测试
var son2 = new Son2('hangyangws');
son2.show(); // 返回：hangyangws
// 分析：（缺点）不能继承父类原型链上的方法
//      （缺点）实例并不是父类的实例，只是子类的实例


// 方法三：组合继承
function Son3(name) {
    Father.call(this, name);
}
Son3.prototype = new Father;
// 分析：（优点）在方法二的基础上，消除“不能继承父类原型链上的方法”缺点
//      （缺点）调用两次父类构造函数，生成两份实例（子类实例将子类原型上的那份屏蔽了）


// 方法四：升级版组合继承（我也不知道叫什么名字了好了^_^）
function Son4(name) {
    Father.call(this, name);
}
Son4.prototype = (new Father()).__proto__;
// 分析：（优点）在方法三的基础上，消除“调用两次父类构造函数”缺点
```

# 函数重载

> js从常理来说是不支持重载的，但是又可以说是天然支持重载  
因为js天然支持可变参数，而且我们在函数内部可以通过arguments对象的length属性，而做出相应的处理  
目前[函数式编程](http://baike.baidu.com/link?url=K_XE6rft1YiCQ9tMPac33DgqW_wdyd6WhjhKR37AbEMCp_Avfnb2oojydKBq4WqrqTSNy9Hjo0giLsK5SO95Top5QUQj0ZVC5ZM4nSK-mysX2qOvoGyFr-Ua2Ne7VAEEdCLId79H_9TkbfqdZFbya_)比较火，所以“重载”已经不再兴起  
在平时项目用得甚少

```javascript
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

# arguments、callee、caller

> 这三种都在严格模式（use strict）下禁用了，开发者请[注意](https://zhidao.baidu.com/question/1385936076596542060.html)

### arguments

> arguments是：函数在调用时，内部创建的一个类似数组的对象

```javascript
function func1() {
    console.log(arguments);
}
function func2(param) {
    console.log(arguments);
}
func1(); // 打印：[]
func1(1, 2); // 打印：[1, 2]
func2(); // 打印：[]
func2(1, 2, 3); // 打印：[1, 2, 3]
// 总结：arguments“长得像数组”
// arguments存储的是：传递给函数的参数，并不局限于函数声明的参数列表，即使没有声明参数也可以
```

### callee

> `callee`是`arguments`的一个属性，表示当前执行的函数

```javascript
function numAdd(num) {
    if (num < 1) {
        return 0;
    }
    return num + arguments.callee(--num);
}
numAdd(3); // 返回：6

// 总结：callee是arguments对象的参数
// arguments.callee就是当前执行的函数
// 可以借助arguments.callee实现**自身调用**或者**递归调用**
// 切记：不要弄成死循环咯^_^
```

## caller

> 每个函数在**执行过程中**都有一个`caller`属性  
表示当前函数执行上下文所在的函数，如果没有则返回`null`

```javascript
(function() {
    function child() {
        // 返回外层的匿名函数，毕竟匿名函数也是函数^_^
        console.log(child.caller);
    }
    child();
})();

function parent() {
    function child() {
        // 返回parent函数，因为child是在parent内部执行的
        console.log(child.caller);
    }
    child();

    // 返回null，因为parent在全局环境执行，并没有“父函数”
    console.log(parent.caller);
};
parent();
```

# 怎么找到this

> 我对this的定义：拥有当前**执行上下文**（context）的一个对象  
开发者需要知道的是：当前的this是哪一个对象  

### 全局环境中找this

> 通常为`window`

```javascript
console.log(this); // 返回：window

function getThis() {
    'use strict';
    console.log(this);
}
getThis(); // 返回：undefined

// 备注：在严格模式下，全局环境this为undefined
// 另外，nodejs环境下，this既不是window也不是undefined，开发者可以自行谷歌
```

### 在执行语句前面有点`•`、 有明确父级执行对象的情况找this

> 是谁在执行语句，语句内部的this就是谁

```javascript
var father = {
    getThis: function() {
        console.log(this);
    }
};

father.getThis(); // 返回：father对象（因为是father在执行getThis函数）

// 注意下面的情况
var myThis = father.getThis;
myThis();// 返回：window

// 上面二行代码可以理解为：
// 定义个全局（window）myThis变量，这个变量指向father.getThis函数
// 在执行myThis时，myThis的父级执行对象是window，所以内部this就为window
```

### 函数内部的函数找this

> 函数内部的函数，没有明确的父级执行对象，this默认绑定到全局

```javascript
var test = {
    getThis: function() {
        var _getThis = function() {
            console.log(this);
        }
        console.log(this);
        _getThis();
    }
}

test.getThis(); // 依次返回：test、window
```

### 存在call、apply和bind的情况找this

```javascript
function getThis() {
    console.log(this);
}

getThis(); // 普通情况，返回：window

var Test = { test: 'test' }; // 定义一个对象：Test

getThis.call(Test); // 返回：Test
getThis.apply(Test); // 返回：Test

var myGetThis = getThis.bind(Test);
myGetThis(); // 返回：Test
```

### 有`new`关键字的情况找this

> new一个对象，对象内部的this就是当前对象  
new的权级要高于bind

```javascript
function getThis() {
    console.log(this);
}

new getThis; // 返回：getThis

var myGetThis = getThis.bind(window);
myGetThis(); // 返回：window
new myGetThis; // 返回：getThis

// 注意上面2行代码
// myGetThis的内部this已经绑定了widnow
// 但是在new过后，内部this还是getThis
```

### ES6的箭头函数找this

> 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象  
箭头函数this指向的固定化，不是因为箭头函数内部有绑定this机制  
而是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this  
正是因为它没有this，所以箭头函数不能用作构造函数

```javascript
var Test = {
    getThis: function() {
        setTimeout(() => {
            console.log(this);
        }, 100);
    },
    getThis2: function() {
        setTimeout(function() {
            console.log(this);
        }, 100);
    }
}

Test.getThis(); // 返回：Test
Test.getThis2(); // 返回：window

// setTimeout的回调参数是普通函数（this在调用时指向全局）
// setTimeout的回调参数是箭头函数 (this在定义时指向Test)
```

# 正则之exec和test

>提示：正则表达式有个属性：`lastIndex`，表示从字符串的哪一个下标开始匹配，默认为`0`

### RegExp.prototype.exec

> exec返回的是数组，如果没有匹配返回为null（注意：不是空数组）  
正则有个属性：lastIndex（默认为0），只有在全局匹配模式才改变

```javascript
var str = 'xxabxxabbxx';

// 普通正则的情况
var reg = /ab*/;
reg.lastIndex; // 返回：0
// 从下标0开始匹配，找到“ab”即返回
reg.exec(str); // 返回：["ab"]
// 因为正则没有定义全局匹配，所以lastIndex不会改变，依旧为0
reg.lastIndex; // 返回：0

// 带有子元素正则情况
var reg = /a(b*)/;
reg.lastIndex; // 返回：0
// 从下标0开始匹配，找到“ab”，数组存入第一个元素；找到“b”，数组存入第二个元素
reg.exec(str); // 返回：["ab", "b"]
// 因为正则没有定义全局匹配，所以lastIndex不会改变，依旧为0
reg.lastIndex; // 返回：0

// 带有子元素且全局配备的情况
var reg = /a(b*)/g;
reg.lastIndex; // 返回：0
// 从下标0开始匹配，找到“ab”，数组存入第一个元素；找到“b”，数组存入第二个元素
reg.exec(str); // 返回：["ab", "b"]
// 因为正则定义了全局匹配，所以lastIndex改为下一次开始匹配的下标
reg.lastIndex; // 返回：4
// 从下标4开始匹配，找到“abb”，数组存入第一个元素；找到“bb”，数组存入第二个元素
reg.exec(str); // 返回：["abb", "bb"]
```

### RegExp.prototype.test

> test方法执行一个检索，用来查看正则表达式与指定的字符串是否匹配，返回 true 或 false  
test类似于 `String.prototype.search()` 方法）  
差别在于test返回一个布尔值，而 search 返回索引（如果找到）或者-1（如果没找到)

```javascript
var str = 'xxabxxabbxx';
var reg = /ab*/;
reg.test(str); // 返回：true

// 注意：
/undefined/.test(); // 返回：true
/undefined/.test('undefined'); // 返回：true
```

# 字符串之match和search

### String.prototype.match

> 正则没有`g`标志，str.match() 返回和 RegExp.exec() 相同  
正则没有`g`标志，返回的 Array 有一个 `input` 属性（解析的原始字符串）  
正则没有`g`标志，返回的 Array 有一个 `index` 属性（匹配结果在原字符串中的索引“以0开始”）  
正则有`g`标志，match返回的是数组，如果没有匹配返回为null（注意：不是空数组）

```javascript
// 没有g的列子
var str = 'OK abc 1.2.3',
    reg = /abc (\d+(\.\d)*)/i;

console.log(str.match(reg));
// 返回：
// [
//    "abc 1.2.3", // 整个匹配
//    "1.2.3",     // 被 (\d+(\.\d)*) 捕获
//    ".3",        // 被 (\.\d) 捕获的最后一个值
//    "index",     // 值为：3。 是整个匹配从 0 开始的索引
//    "input"      // 值为：'OK abc 1.2.3'。被解析的原始字符串
// ]

// 有g的列子
var str = 'ABCDabcd',
    reg = /[A-C]/gi;
console.log(str.match(reg));
// 返回：["A", "B", "C", "a", "b", "c"]
```

> 如果match参数为非正则表达式对象，则会隐式地使用 new RegExp(obj) 将其转换为一个 RegExp  
如未提供参数，那么你会得到一个包含空字符串的 Array ：[""]

```javascript
var str = "+Infinity 10";
str.match(Infinity); // 返回：["Infinity"]
str.match(+10); // 返回：["10"]
str.match(); // 返回：[""]
```

### String.prototype.search


[参考地址](http://blog.csdn.net/z69183787/article/details/17886369)

# call、bind、apply

# promise及原理

# fetch

# 位运算符

> & |


# IIFE

> [参考](http://rensanning.iteye.com/blog/2080429)  
IIFE（immediately invoked function expression）  
IIFE又称为**自执行函数**、**立即执行函数**  
我们知道函数需要“调用”，才能执行，比如`var func = function() {}; func(); // 调用`


# 闭包

> 闭包实际上设计一个对象的属性，何时被gc处理的问题 闭包和gc是相关联的

# 数组相关

### 数组的长度是根据下标的最大而确定的

```javascript
var arr = [];
arr['test'] = 'test'; // 数组的下标可以死字符串
arr.length; // 返回：0 // 字符串下标不计入数组长度
arr[10] = 10;
arr.length; // 返回：11
```

### 手动赋值数组长度可以删减多余元素

```javascript
var arr = [1, 2, 3, 4];
arr.length = 2;
console.log(arr); // 返回：[1, 2]
```