**写在前面**

分享目的：「攻巩固 `CSS` 知识，发现新的『桃花源』」  
受众群体：「web 前端开发者、爱好者」

感谢：

1. [俊哲](https://github.com/lcjnil) 推荐的 ppt：[如何做一个技术分享](https://docs.google.com/presentation/d/1dEiloN8jX5KUIorz12fSSTADAWupArMVpIHzIcBaqBA/edit#slide=id.g241a7f5a41_0_42)
1. [www.w3.org](https://www.w3.org) 文献
1. [张鑫旭](www.zhangxinxu.com) 个人博客文献

# 我遇见的哪些 CSS 中有趣的尺寸、宽高

### 不常见长度单位

- `ex` 相对于「小写字母」`x` 的 **高度**
- `ch` 相对于「数字」 `0` 的 **宽度**

[can i use](http://caniuse.com/#feat=ch-unit)

利用 `ch` 单位实现「打字效果」的 [一个 Demo](http://hangyangws.win/demos/apps/css/ch-typing/)

- vw 相对于视窗的 **宽度**：视窗宽度是100vw「window.innerWidth」
- vh 相对于视窗的 **高度**：视窗高度是100vh「window.innerHeight」
- vm 取决于 `min(vw, vm)`

[can i use](http://caniuse.com/#feat=viewport-units)

### 实用的实体单位

- `&emsp;` 相当于 em 的宽度
- `&ensp;` 相当于 1/2 em 的宽度

`&ensp;` 屏蔽了 `letter-spacing` 会使 `last-letter` 后面也出现间距的弊端  
利用 `&emsp;` 实现的对齐效果 [一个 Demo](http://hangyangws.win/demos/apps/html/emsp/)  
另外 `text-align: justify;` 也能实现「文本两端对齐」的效果 [一个 Demo](http://hangyangws.win/demos/apps/html/justify/)

### height、width、百分比、循环

先抛出一个疑问：如果没有显示的设置父元素宽高，子元素宽高的百分比有效果吗？  
[看一个 Demo](http://hangyangws.win/demos/apps/html/percentage_w_h/)

总结 [w3 对高度的定义](https://www.w3.org/TR/CSS21/visudet.html#propdef-height) 、[w3 对宽度的定义](https://www.w3.org/TR/CSS21/visudet.html#blockwidth)：  
**高度的计算**  
如果元素 **没有显示的设置高度** 且 **非 fixed/absolute** 定位，  
其 **渲染高度** 为子元素的的高度，其 **计算高度** 为 `auto`  
所以未显示设置高度，其高为 auto，子元素 `height: 100%` 的意思就是 `height ≈ auto * 100% ≈ auto`

**宽度的计算**：  
如果元素 **没有显示的设置宽度** 且 **非 fixed/absolute** 定位，  
if (element.style.display ≈ block) {  
  其 **渲染宽度** 为父元素的的宽度，其 **计算宽度** 也为父元素的的宽度  
}  
if (element.style.display ≈ inline-block) {  
  其 **渲染宽度** 为子元素的的宽度，其 **计算宽度** 也为子元素的的宽度  
}
所以未显示设置宽度，其高为和 `渲染高度` 一样，所以子元素的百分比宽度有效果

再抛出一个疑问：[这 Demo](http://hangyangws.win/demos/apps/html/percentage_w_h/) 的父元素的宽为什么不是子元素的宽度和  
如果父元素宽度变化，这样会不会带来渲染循环问题？

答案是不会：  
浏览器渲染的基本原理

1. 下载文档内容
1. 加载头部的样式资源
1. 按照从上而下，自外而内的顺序渲染DOM内容「先渲染父元素，后渲染子元素」

所以 **父元素选择器** 久久未实现，可能是因为这样会导致「循环渲染」

### padding 百分比的小妙招

抛出一个问题：padding-top、padding-bottom 如果为百分比的计算方式？  
可以基于这个效果实现等比效果

### height:100% 和 height:inherit 的异同

绝对定位元素：  
`height:inherit` 为父元素；`height:100%` 为定位基准元素

### width 新鲜值

方便某些布局的实现，  
作用： 在原有的 display 水平不变的情况下拥有元素其他 display 值才有的特性

- fill-available

块级元素默认就是 fill-available
[一个 Demo 认识 fill-available](http://hangyangws.win/demos/apps/css/width/fill-available/)

- max-content

**假设** 我们的容器有足够的宽度，足够的空间，此时，所占据的宽度是就是 max-content所表示的尺寸  
[一个 Demo 认识 max-content](http://hangyangws.win/demos/apps/css/width/max-content/)
[一个 max-content 的实际用力](http://hangyangws.win/demos/apps/css/width/max-content-2/)


- min-content：

- fit-content：

