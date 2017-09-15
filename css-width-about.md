**写在前面**

分享目的：「攻巩固 `CSS` 知识，发现新的『桃花源』」  
受众群体：「web 前端开发者、爱好者」

感谢：

1. 俊哲推荐的 ppt：[如何做一个技术分享](https://docs.google.com/presentation/d/1dEiloN8jX5KUIorz12fSSTADAWupArMVpIHzIcBaqBA/edit#slide=id.g241a7f5a41_0_42)
1. [www.w3.org](https://www.w3.org) 文献
1. [张鑫旭](www.zhangxinxu.com) 个人博客文献

# 我遇见的哪些 CSS 中有趣的尺寸、宽高

### 长度单位

[link](http://www.zhangxinxu.com/wordpress/2012/09/new-viewport-relative-units-vw-vh-vm-vmin/)

- ex 相对于小写字母「x」的高度
- ch 相对于数字「0」尺寸

CSS [打字特效](http://www.zhangxinxu.com/study/201412/animation-border-background-dot-dot-dot-wait.html)  
[link - 等宽字体在web布局中应用以及CSS3 ch单位嘿嘿](http://www.zhangxinxu.com/wordpress/2016/07/monospaced-font-css3-ch-unit/)  
[can i use](http://caniuse.com/#feat=ch-unit)

- vw 相对于视窗的宽度：视窗宽度是100vw
- vh 相对于视窗的高度：视窗高度是100vh
- vm 相对于视窗的宽度或高度，取决于哪个更小

Chrome浏览器下浏览器窗体改变可能的不渲染bug  
[can i use](http://caniuse.com/#feat=viewport-units)

### 实体单位

&emsp;&ensp;

text-align: justify;

### height 百分比 与循环问题

元素没有格式化的高度值，子元素的height百分比高度是不起作用
疑问：为什么宽度可以，高度不可以？？？
[link](https://stackoverflow.com/questions/2239045/why-is-100-height-not-100-of-the-browser-height)

[w3 对高度的定义](https://www.w3.org/TR/CSS21/visudet.html#propdef-height)
[w3 对宽度的定义](https://www.w3.org/TR/CSS21/visudet.html#blockwidth)

浏览器渲染的基本原理：
1. 下载文档内容
1. 加载头部的样式资源
1. 按照从上而下，自外而内的顺序渲染DOM内容「先渲染父元素，后渲染子元素」

展示 demo

疑问：为什么没有父元素选择器「那么真的循环开始了」


[link - 从height:100%不支持聊聊CSS中的“死循环”](http://www.zhangxinxu.com/wordpress/2016/09/talking-about-css-infinite-endless-loop/)

### padding 百分比 等比

### height:100%和height:inherit的异同

### width 的新鲜值 !!!

[link - mdn](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width)
[link - 理解CSS3 max/min-content及fit-content等width值](http://www.zhangxinxu.com/wordpress/2016/05/css3-width-max-contnet-min-content-fit-content/)
