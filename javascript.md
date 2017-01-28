# javascript

- ### 数据类型
    - 6种原始值（不可变。“除非重置当前变量，否则不能改变元素值。”）
        1. Null(只有一个值： null)
        1. Undefined(一个没有被赋值的变量会有个默认值 undefined)
        1. Number
        1. Boolean(两个值：true 和 false)
        1. String
        1. [Symbol](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
    - 和Object(对象指内存中的可以被标识符引用的一块区域)

- ### 数据类型检测之`typeof`
    - typeof(对变量或值调用 typeof 运算符将返回(字符串)下列值之一)
        1. undefined - Undefined类型
        1. number - Number类型
        1. boolean - Boolean类型
        1. string - String类型
        1. symbol - Symbol类型(ECMAScript6新增)
        1. function - 函数对象([[Call]]在ECMA-262条款中实现了)
        1. object - 引用类型 或 Null类型
    ```javascript
    typeof(Function) // function (Function是函数对象)
    typeof(new Function) // function (new Function也是是函数对象，同等：var func = function(){})
    typeof(Array) // function (Array是函数对象)
    typeof(new Array) // object（实例化的Array就是object）
    ```

- ### 变量赋值时候的返回值
    ```javascript
    var name = 'hangyang'; // 返回：undefined
    name = 'ws'; // 返回：ws
    ```
    > 结语：定义变量的时候赋值返回:undefined。
    > 给已声明变量赋值时候返回当前赋值。

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
    // 第一轮是对n-1的位置定位
    // 第二轮是 每一个位置的数的 确定
    var arr = [1, 4, 5, 6, 99, 111, 112, 113, 133],
        temp = 0,
        flag = false;
    for (var i = 0; i < arr.length - 1; i++) {
        document.writeln('come');
        for (var j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                flag = true;
            }
        }
        if (flag) {
            flag = false;
        } else {
            break;
        }
    }
    for (var i = 0; i < arr.length; i++) {
        document.writeln(arr[i]);
    };
    ```

- ### 二分查找法
    ```javascript
    var arr = [41, 55, 76, 87, 88, 99, 123, 432, 546, 577, 688, 786];

    function twoFind(arr, wantVal, leftIndex, rightIndex) {
        if (leftIndex > rightIndex) {
            document.writeln('SORRY: 找不到 ' + wantVal + ' ！');
            return;
        }
        var minIndex = Math.floor((leftIndex + rightIndex) / 2);
        if (arr[minIndex] > wantVal) {
            twoFind(arr, wantVal, leftIndex, minIndex - 1);
        } else if (arr[minIndex] < wantVal) {
            twoFind(arr, wantVal, minIndex + 1, rightIndex);
        } else {
            document.writeln('找到了 ' + wantVal + ' ,下表为' + minIndex);
        }
    }
    twoFind(arr, 9, 0, arr.length - 1);
    ```

- ### arguments、callee、caller
    ```javascript
    ```

- ### call、bind、apply
    ```javascript
    ```

- ### 函数（类）的继承与重载
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
            this.Father(name, age); // 执行Son内部的Father函数，等同于吧代码A和代码B之间的代码执行了一遍，因而实现“继承”。
        }
        var me = new Son('hangyangws', 21);
        me.name; // hangyangws
        me.show(); // hangyangws 21
        ```
    - 重载
        > js从常理来说是不支持重载的，但是又可以说是天然支持重载，因为js天然支持可变参数，而且我们在函数内部可以通过arguments对象的length属性，而做出相应的处理。
        > 目前[函数式编程](http://baike.baidu.com/link?url=K_XE6rft1YiCQ9tMPac33DgqW_wdyd6WhjhKR37AbEMCp_Avfnb2oojydKBq4WqrqTSNy9Hjo0giLsK5SO95Top5QUQj0ZVC5ZM4nSK-mysX2qOvoGyFr-Ua2Ne7VAEEdCLId79H_9TkbfqdZFbya_)比较火，所以“重载”已经不再兴起。

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

- ### 闭包
    > 闭包实际上设计一个对象的属性，何时被gc处理的问题 闭包和gc是相关联的。

    ```javascript
    ```

- ### 数组相关
    - 长度（length属性）

        ```javascript
        // 数组的长度是根据下标的最大而确定的
        var arr = new Array();
        arr['one'] = 'one';
        arr['two'] = 'two';
        arr.length; // 返回：0
        arr[100] = 100;
        arr.length; // 返回：101
        ```
