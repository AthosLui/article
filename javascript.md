# javascript

---

- 数字的固定小数位数
    ```javascript
    var a=8.88888,b=9.88,c=9.00,d=4.4,e=7;
    document.writeln('num.toFixed(num)');
    document.writeln(a.toFixed(2));
    document.writeln(b.toFixed(2));
    document.writeln(c.toFixed(2));
    document.writeln(d.toFixed(2));
    document.writeln(e.toFixed(2));
    ```

- js 中 在函数内 定义变量 有var表示在函数体内有效 反之是用全局
    ```javascript
    var a = 2;

    function abc() {
        a = 3;
    }
    abc();
    window.alert(a);

    function abd() {
        var a = 5;
    }
    abd();
    window.alert(a);
    ```
- 数组长度 和定义 js 是编译语言 数组长度是随时程序变化而变化的
    ```javascript
    var arr = [1, 2, 3];
    for (var i = 0; i < arr.length; i++) {
        document.writeln(arr[i]);
    }
    arr[9] = 10;
    for (var i = 0; i < arr.length; i++) {
        document.writeln(arr[i]);
    }
    alert(arr.length);
    ```

- js 的对话框输入框 prompt 和 字符串分开函数 split
      // slit 的第二个参数可以不要 其表示取前几个值？
        var arr=window.prompt('请输入你想想加的数字 以空格为界限');
        arr=arr.split(" ",2);
        var sum=0;
        for (var i = 0; i < arr.length; i++) {
            sum+=parseInt(arr[i]);
        }
        window.alert(parseInt(sum));


        // 数组的循环输出可以用键值 for in 循环
      var arr=[1,2,3];
        for ( var k in arr ) {
            document.writeln(k+'--->'+arr[k]);
        }


        // 矩阵的转置
      var arr = [[1,2,3,4],[5,6,6,6],[7,6,7,8],[8,5,3,3]];
        for (var i = 0; i < arr.length; i++) {
            for (var j = 0; j < arr[i].length; j++) {
                document.writeln(arr[i][j]);
            }
            document.writeln('<br />');
        }
        var c;
        changeArr(arr);
        function changeArr (arr) {
            for (var i = 1; i < arr.length; i++) {
                for (var j = 0; j < i; j++) {
                    c=arr[i][j];
                    arr[i][j]=arr[j][i];
                    arr[j][i]=c;
                }
            }
        }
        document.writeln('<br />');
        for (var i = 0; i < arr.length; i++) {
            for (var j = 0; j < arr[i].length; j++) {
                document.writeln(arr[i][j]);
            }
            document.writeln('<br />');
        }
        // 冒泡排序方法
        // 第一轮是对n-1的位置定位


        // 第二轮是 每一个位置的数的 确定
      var arr=[1,4,5,6,99,111,112,113,133],temp=0,flag=false;
        for (var i = 0; i < arr.length-1; i++) {
            document.writeln('come');
            for (var j = 0; j < arr.length-1-i; j++) {
                if (arr[j]>arr[j+1]) {
                    temp=arr[j];
                    arr[j]=arr[j+1];
                    arr[j+1]=temp;
                    flag=true;
                }
            }
            if (flag) {
                flag=false;
            } else {
                break;
            }
        }
        for (var i = 0; i < arr.length; i++) {
            document.writeln(arr[i]);
        };


        // 二分查找
      var arr=[41,55,76,87,88,99,123,432,546,577,688,786];
        function twoFind (arr,wantVal,leftIndex,rightIndex) {
            if (leftIndex > rightIndex) {
                document.writeln('SORRY: 找不到 '+wantVal+' ！');
                return;
            }
            var minIndex=Math.floor((leftIndex+rightIndex)/2);
            if (arr[minIndex]>wantVal) {
                twoFind(arr,wantVal,leftIndex,minIndex-1);
            } else if (arr[minIndex]<wantVal) {
                twoFind(arr,wantVal,minIndex+1,rightIndex);
            } else {
                document.writeln('找到了 '+wantVal+' ,下表为'+minIndex);
            }
        }
        twoFind(arr,9,0,arr.length-1);


        // 一切都是对象
      var a=3;
        if (a instanceof Number) {
            window.alert('a 是数字');
        }else {
            window.alert(a.constructor);
        }

        if (a.constructor==Number) {
            window.alert('a 是数字');
        }else {
            window.alert(a.constructor);
        }


        // js 对象访问属性的二种方式
      function Person () {};
        var new1 = new Person ();
        new1.name='冯杰';
        new1.age=21;
        window.alert(new1.name);
        window.alert(new1["age"]);


        // js delete 只能 删除对象的属性
      function Person () {};
        var me = new Person();
        me.name='冯杰';
        window.alert(me.name);
        delete me.name;
        window.alert(me.name);


        // js this的使用
      function Person () {
            this.name="冯杰";
            this.age=21;
        }
        var p1 = new Person();
        var p2 = new Person();
        p2.name='fj'
        window.alert(p1.name);
        window.alert(p2.name);
        // js 类里面的变量的共有和私有


        // js 里面访问私有属性 就定义一个公开方法
      function Person () {
            this.name = 'fj';//这样写表示共有
            var age = 21;//这样写表示私有 私有的属性 只有 公共函数（方法）才能访问
            this.getAge =  function ()　{//这样写表示共有的方法
                // window.alert(age);
                // return this.age;
                getName();
            }
            function getName () {//这样写表示私有的方法 私有的方法也只有通过共有的方法访问
                // return this.name;
                window.alert(age);
            }
        }
        var me = new Person();
        // window.alert(me.getAge);
        me.getAge();


        // js 里面默认的对象的window 那个对象调用this所在的函数 this 就指向这个对象
      var a=22;
        window.alert(a);
        window.alert(window.a);
        // 上面的2句是一样的意思
        alert('dd');
        window.alert('dd');
        // 上面的2句是一样的意思
        function aFunction () {
            document.writeln('dd');
        }
        aFunction();
        window.aFunction();
        // 上面的2句是一样的意思


        // 在js 中 对象的方法不是通用的 如果生成n个对象 那么就有n个内存堆栈
        // js 中 一切类 继承自 Object 而Object 有propotype
        // 下面是解决办法 prototype 获得类的static性质
      function God () {}
        God.prototype.shout=function () {
            window.alert('小狗叫');
        }
        var dog1= new God();
        var dog2= new God();
        dog1.shout();
        dog2.shout();


        // js里要想创建对象 除了一般的创建方式 还有 通过Object 方式创建类
        // Object 类是所有js类的基类 Object 就表示对象（一切的对象）
      var p1 = new Object();
        p1.name='fj';
        window.alert(p1.name);
        window.alert(p1.constructor);


        // 小实验1
      var num=new Number(1);
        // var num2=10;
        // window.alert(num.constructor);
        // window.alert(num2.constructor);
        // 上面2个弹出是一样的
        Number.prototype.add = function(a){//prototype是属于类的
            return this+a;
        }
        window.alert(num.add(1).add(2));


        // 小实验2 Array.reverse() 颠倒数据
      var arr = new Array(3);
        arr[0]='fj0';
        arr[1]='fj1';
        arr[2]='fj2';
        for (var key in arr) {
            document.writeln(key+'-->'+arr[key]+'&nbsp;&nbsp;&nbsp;&nbsp;');
        }
        document.write('<br />');
        arr.reverse();
        for (var key in arr) {
            document.writeln(key+'-->'+arr[key]+'&nbsp;&nbsp;&nbsp;&nbsp;');
        }


        // 小实验 为Array 添加 find(val) 方法
      Array.prototype.find = function (a) {
            for (var i = 0; i < this.length; i++) {
                if (this[i] == a) {
                    return i;
                }
            }
            return 'find fail.';
        }
        var arr=[0,1,2,77,4,5];
        window.alert(arr.find(77));

        // js里面没有重载的概念
        // 相同的方法 会被覆盖
      function test (a) {
            window.alert(a);
        }
        function test (a,b) {
            window.alert(a+'--'+b);
        }
        test(1);


        // js 直接定义变量和函数 就是表示全局的函数和变量 是属于windows的
      var a=1;
        function function1 () {
            a++;
            window.alert(a);
        }
        window.a++;
        window.function1();

        // js 函数可以知道来的参数的数量
        // 方法有个删除数组 arguments[]
      function abc () {
            var sum=0;
            for (var i = 0; i < arguments.length; i++) {
                sum+=arguments[i];
            }
            return sum;
        }
        window.alert(abc(1,2,3));

        // js 函数也可以作为参数传递
      function jisuan (a,b) {
            return a+b;
        }
        function Person(name,age,fun) {
            this.name=name;
            this.age=age;
            this.fun=fun;
        }
        var fj=new Person('fj','21',jisuan);
        window.alert(fj.name);
        window.alert(fj.fun(1,2));

        // js 里面类 还有一种定义方法
      var Person={
            name: 'fj',
            age: 21,
            sing: {
                songa:'我只在乎你',
                songb:'I\'m an angel.',
                showSong:function(){
                    alert(this.songa+'---'+this.songb);
                }
            }
        }
        window.alert(Person.name);
        Person.sing.showSong();

        // js 里面call函数目的就是改变对象的this指向
      var Person={
            name:'fjj'
        };
        function test() {
            window.alert(this.name);
        }
        test.call(Person);


        // 用 for in 遍历window对象
      document.write('****************当前浏览器的window的所有方法和属性****************<hr />');
        for(var k in window){
            document.write(k+':'+window[k]+'<hr />');
        }

        // 体会js的封装
      function Person () {
            var name='fj';//私有
            this.age=21;//共有
        }
        var p1 = new Person();
        window.alert(p1.name);//undefined
        window.alert(p1.age);//21

        // js 的prototype 的方法不能访问私有属性和方法
      function Person () {
            var name='fj';//私有
            this.age=21;
        }
        Person.prototype.showName=function(){
            window.alert(this.name);
        }
        Person.prototype.showAge=function(){
            window.alert(this.age);
        }
        var p1=new Person();
        p1.showName();
        p1.showAge();


        // js 里面是对象冒充来继承的 不算是真正的继承 通过对象冒充 js可以实现多重继承和继承的效果 但是没有Extends关键字
      function Father (name,age) {
            this.name=name;
            this.age=age;
            this.show=function(){
                window.alert(this.name+'---'+this.age);
            }
        }
        function Son (name,age) {
            this.Father=Father;
            this.Father(name,age);//通过对象冒充 实现继承 这一句非常重要 js是动态语言 不是编译语言 要执行才会分配空间
        }
        var me=new Son('fj',21);
        window.alert(me.name);
        me.show();

        // 重载 js从常理来说是不支持重载的 但是又可以说是天然支持重载 因为js天然支持可变参数 而且我们可以通过arguments[]数组的长度判断 而做出相应的处理
        // 闭包实际上设计一个对象的属性，何时被gc处理的问题 闭包和gc是相关联的

        // js内部类有静态和动态二种
      var date=new Date();
        window.alert(new Date());
        window.alert(date.toLocaleString());
        window.alert(date.getYear);


        // 数组的长度是根据下标的最大而确定的
      var arr= new Array ();
        arr['a']=1;
        arr['b']=2;
        window.alert(arr.length);//打出0


        // toString 转字符串 但是对数字带来 toString(val) 其中val可以指定规定的进制数 什么都不写就是十进制
      var a=44;
        window.alert(a.toString(2));

    </script>
    <style>

        body {
            margin: 0
        }

        div {
            padding: 5%;
            margin: 25% auto;
            font-family: '微软雅黑';
            font-size: 50px;
            color: #fff;
            letter-spacing: 2px;
            text-align: center;
            background-color: #666
        }
    </style>
</head>
<body>
    <div>本页讲述 JS 的一些用法和小知识<hr />学习可在源码查看</div>
</body>
</html>