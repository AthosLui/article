[查看其他文章](https://github.com/hangyangws/myArticles#articles-list)

# front-end-summary

- ### LazyMan
    - 实现LazyMan（什么是LazyMan？请自行google）
    ```javascript
    function _LazyMan(_name) {
        var _this = this; // 缓存this
        _this.tasks = []; // 任务初始化为空数组
        _this.tasks.push(function() {
            console.log('Hi! This is ' + _name + '!');
            // 当前匿名函数，没有明确的执行对象，所以函数里面的this指向window，因此访问当前LazyMan对象就要缓存this
            _this.next();
        });
        // setTimeout会开辟另一个执行临时队列，在当前线程（js是单线程）执行完成后才会执行此临时队列的任务。
        // 在执行此临时队列时，会按照先前设置时间延迟。
        // 如果延迟时间设置为0，就以为着不延迟执行。
        // 这样做的意义在于：让当前任务脱离当前执行的线程（有点异步执行的感觉）
        setTimeout(function() {
            _this.next(); // 执行下一个任务
        }, 0);
    }

    // push函数里面的this和setTimeout函数里面的this都指向全局作用域，所以要缓存当前this指向
    _LazyMan.prototype.next = function() {
        // 取出任务队列的任务存入变量
        var _fn = this.tasks.shift();
        // 如果当前任务存在，就执行当前任务。（&&左边为真在会去执行右边，有点if语句的感觉）
        _fn && _fn();
    }
    _LazyMan.prototype.sleep = function(_time) {
        var _this = this;
        _this.tasks.push(function() {
            setTimeout(function() {
                console.log('Wake up after ' + _time);
                _this.next();
            }, _time);
        });
        return _this;
    }
    _LazyMan.prototype.sleepFirst = function(_time) {
        var _this = this;
        // sleepFirst和sleep原理一样，只是在新增任务时插队了，把当前任务放在了队列的最前面
        _this.tasks.unshift(function() {
            setTimeout(function() {
                console.log('Wake up after ' + _time);
                _this.next();
            }, _time);
        });
        return _this;
    }
    _LazyMan.prototype.eat = function(_eat) {
        var _this = this;
        _this.tasks.push(function() {
            console.log('Eat ' + _eat);
            _this.next();
        });
        return _this;
    }

    // 封装对象
    var LazyMan = function(_name) {
        return new _LazyMan(_name);
    }

    // 运行测试
    LazyMan('hangyangws').eat('apple').sleep(1000).sleepFirst(2000);
    // 结果:
    // "Wake up after 2000"(2s后输出)
    // "Hi! This is hangyangws!"
    // "Eat apple" "Wake up after 1000"(1s后输出)
    ```

- ### 用JS求出元素的最终的`background-color`，不考虑元素float、absolute情况。
    > widow.getComputedStyle (获取css中设置的样式，'准浏览器'。返回的对象中，驼峰命名和中划线命名的都有，如：`background-color`和`backgroundColor`都有。
    > element.style (获取的是元素行间设置的样式)
    > element.currentStyle (ie低版本)

    ```javascript
    // 获取指定元素的某个CSS样式，兼容IE
    var getStyle = function($el, _attr) {
        if(window.getComputedStyle) {
            return window.getComputedStyle($el, null)[_attr]
        }
        if($el.currentStyle) {
            return $el.currentStyle[_attr];
        }
        return $el.style[_attr];
    }

    var getBG = function($el) {
        var color = getStyle($el, 'backgroundColor');
        if(color === 'rgba(0, 0, 0, 0)' || color === 'transparent') { // 判断是否透明
            return $el.tagName === 'HTML' ? 'rgb(255, 255, 255)' : arguments.callee($el.parentNode, 'backgroundColor');
        } else {
            return color;
        }
    }
    ```

- ### 前端优化简述

    > 应用优化涉及各个方面，前端优化只是冰山一角。有人说：“离开系统的性能瓶颈的前端优化都是扯蛋”，我觉得，我们各司其职，做好前端本职工作就好，不要好高骛远。

    - 优化目的
        1. 用户角度：页面加载更快、操作响应更快、体验更好
        1. 服务端角度：减少请求数、减小请求带宽
    - 优化方法
        1. 页面优化
            - HTTP请求数
                1. 从设计实现层面简化页面
                1. 合理设置`HTTP`缓存
                1. 资源合并与压缩(example：`CSS Sprites`)
                1. Inline Images（将图片嵌入到页面或style文件）
                1. Lazy Load Images
                1. 避免重复的资源请求
            - 资源的无阻塞加载
                1. CSS放在HEAD中
                1. JavaScript置底
                1. Lazy Load Javascript（example：`AMD`）
        1. 代码优化
            - DOM操作优化
                1. 减少DOM操作，减少`Reflow和Repaint`
                1. HTML Collection（类数组集合。并不是一个静态的结果，表示的仅是特定的查询，每次访问时会重新执行查询。需要遍历 HTML Collection时，将它转为数组再访问，以提高性能。）
            - JavaScript
                1. 减少作用域链查找（example：缓存全局变量）
                1. 慎用 `with、eval、Function`
                1. 减少闭包的使用（易内存浪费，不仅仅是常驻内存，重要的是，使用不当会造成无效内存的产生）
                1. 直接量、局部变量的使用（对象属性以及数组的访问需要更大的开销）
                1. 减少字符串拼接`+`使用
            - CSS选择符优化
                1. 减少层级，多用class（浏览器解析CSS是从右往左）
            - 资源优化
                1. 图片格式的选择（非透明大图尽量不用png、PS保存图片为`web格式`且勾选`连续`选项）
            -  HTML结构优化
                1. 使用HTML5 DOCTYPE
                1. 标签闭合、结构分离
                1. Boolean 属性不需要赋值，如果存在则为True（example：`checked、selected`）
                1. 语义化、标签统一整洁
                1. 减少文本和元素混合，并作为另一元素的子元素
                1. 避免使用`<br />、<hr />`

- ### 跨域访问之JSONP

    > - 同源策略`same-Origin-Policy`：指浏览器对不同源的脚本或文本的访问方式进行的限制。
    > - 同源：指两个页面具有相同的**协议**、**主机`也常说域名`**、**端口**三要素缺一不可。
    > - 所以在JS代码中访问不同源的数据会提示”跨域警告“，但是浏览器的`<script>`标签可以加载不同源的数据，这样就给我们“可乘之机”：使用**JSONP**跨域。
    > - JSONP（JSON with Padding）的基本原理：在HTML页面中创建`<script>`节点，向不同源提交网络请求，实现跨域。

    - HTML页面中创建`<script>`节点

        ```javascript
        var script = document.createElement('script'); // 创建<script>节点
        script.src = 'http://example.com/getData'; // 添加src属性
        document.getElementsByTagName('HEAD')[0].appendChild(script); // 插入节点到head头
        ```
    - 数据返回
        - 我们知道`XMLHttpRequest`对象有`onreadystatechange`方法，在请求成功后可以获取`responseText`内容。
        - 但是问题来了，使用`JSONP跨域`如何拿到返回的数据，拿到返回的数据后如何立即调用。
        - 解决方案是：
            1. 创建一个函数，函数参数为服务端板返回的数据。

                ```javascript
                function callBack(responseText) {
                    // 操作responseText
                }
                ```
            1. 给script的src属性设置一个参数。比如：`http://example.com/getData?name="callBack"`。
            1. 服务端接受到GET数据：`name="callBack"`，得到`callBack`函数名。
            1. 服务端以**函数调用**的方式返回数据：

                ```javascript
                callBack({example: 123})
                ```
            1. 浏览器端得到数据：`callBack({example: 123})`。
            1. 浏览器执行数据：`callBack({example: 123})`。
            1. 这个时候我们预先设置好的`callBack`函数就被已“回调函数”的方式调用了。
    - JSONP优点
        - 与`XMLHttpRequest`不同，JSONP不受同源策略限制。
        - IE支持良好。
        - 在请求完成后可通过callback的方式传回结果。
    - JSONP不足
        - 只支持get请求，不支持post请求。
        - 服务端需要根据客户端传过来函数名返回数据。
        - 只支持网络跨域的请求数据，不能解决不同域的两个页面之间如何进行JS调用的问题。

- ### 获取元素距离页面的top、left
    ```javascript
    function getRec(ele) {
        var _t = document.documentElement.clientTop,
            _l = document.documentElement.clientLeft,
            rect = ele.getBoundingClientRect();
        return {
            top: rect.top - _t,
            right: rect.right - _l,
            bottom: rect.bottom - _t,
            left: rect.left - _l
        }
    }
    ```
    > 注意：IE、Firefox3+、Opera9.5、Chrome、Safari支持，在IE中，默认坐标从(2,2)开始计算，导致最终距离比其他浏览器多出两个像素，我们需要做个兼容。

- ### 矩阵的转置
    ```javascript
    var arr = [ // 定义一个矩阵（二维数据）
        [1, 2, 3, 4],
        [5, 6, 6, 6],
        [7, 6, 7, 8],
        [8, 5, 3, 3]
    ];

    function changeArr(arr) { // 矩阵转置函数
        var c;
        for (var i = 1; i < arr.length; i++) {
            for (var j = 0; j < i; j++) {
                c = arr[i][j];
                arr[i][j] = arr[j][i];
                arr[j][i] = c;
            }
        }
    }
    changeArr(arr);
    console.table(arr);
    ```

- ### 冒泡排序法
    ```javascript
    function bubbleSort(_arr) {
        var _len = _arr.length - 1,
            _index_out = 0,
            _index_in,
            _temp,
            _flag;
        if (_len > 0) {
            while (_index_out < _len) {
                _flag = false;
                _index_in = 0; // 内层循环每次要从0开始
                while (_index_in < _len - _index_out) {
                    if (_arr[_index_in] > _arr[_index_in + 1]) {
                        // 两者值交换
                        _temp = _arr[_index_in];
                        _arr[_index_in] = _arr[_index_in + 1];
                        _arr[_index_in + 1] = _temp;
                        _flag = true;
                    }
                    _index_in++;
                }
                if (!_flag) {
                    // 如果数组已经是顺序的，就不必再循环了
                    break;
                }
                _index_out++;
            }
        }
        return _arr;
    }
    ```

- ### 二分查找法
    ```javascript
    /**
     * @param  {[Array]}  _arr         [查找的数组]
     * @param  {[Number]} _wantVal     [查找的值]
     */
    function binarySearch(_arr, _wantVal) {
        // 二分查找的前提是数组应该是有序的
        var _left = typeof arguments[2] !== 'undefined' ? arguments[2] : 0,
            _right = typeof arguments[3] !== 'undefined' ? arguments[3] : _arr.length - 1;
        if (_left > _right) {
            // 没有找到相应值
            return null;
        }
        var _middleIndex = Math.floor((_left + _right) / 2);
        if (_arr[_middleIndex] > _wantVal) {
            // 查找的值在左边
            return binarySearch(_arr, _wantVal, _left, _middleIndex - 1);
        }
        if (_arr[_middleIndex] < _wantVal) {
            // 查找的值在右边边
            return binarySearch(_arr, _wantVal, _middleIndex + 1, _right);
        }
        // 找到要查找的值
        return _middleIndex;
    }
    ```

- ### 快排算法
    ```javascript
    ```

- ### CSS下载解析会不会阻塞DOM树渲

- ### 以什么为基准去衡量什么时候使用base64

- ### HTTPS和HTTP有什么区别

- ### SSL四次握手过程

- ### TCP三次握手过程

- ### SSL握手时有对称加密和非对称加密吗

- ### CSS inline

- ### 盒模型(W3C和IE)

- ### flex的使用

- ### CSS hack技术

- ### 从输入url到渲染的整个过程?

- ### 懒加载&&预加载

- ### 如果父元素的font-size也是采用em表示，那么子元素的font-size怎么计算等?

- ### margin重叠现象与BFC

- ### bootstrap的基本原理，bootstrap的grid系统。

- ### 浅复制 && 深复制。
    - 有什么区别
    - 如何实现Object的深复制`递归的方法进行复制/循环的方法`

- ### xss和csrf
