- 用JS求出元素的最终的`background-color`，不考虑元素float情况。
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

    }
    ```