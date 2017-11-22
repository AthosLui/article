[link for w3cPlus](https://www.w3cplus.com/blog/tags/411.html?page=2)

[SVG入门](http://www.bestvist.com/2017/11/08/svg/)
[CSS 并不简单--实例带你领略实现SVG动画的姿势](https://juejin.im/post/596894586fb9a06bbc4b0f5a)
[腾讯实例教学！带你轻松打开SVG动画的大门](http://www.uisdc.com/tencent-svg-animation-design)
[SVG 新司机开车指南](https://zhuanlan.zhihu.com/p/25016633)

[SVG动画案例的学习](https://www.w3cplus.com/svg/an-svg-animation-case-study.html)
[一个例子上手SVG动画](https://aotu.io/notes/2017/05/04/example-for-svg-animation/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)
[SVG 实现动态模糊动画效果](http://web.jobbole.com/92983/)
[线条之美，玩转SVG线条动画](https://www.nihaoshijie.com.cn/index.php/archives/667/)
[一个比想象中更骚气的圆-svg实现](https://juejin.im/post/578218ac5bbb500061fffa85)
[使用 SVG 蒙版 (mask) 来实现波浪 (wave) 动画效果](http://svgtrick.com/tricks/554e3452640d3aea8b0b48d90eb71fe7)
[让文字沿着路径动起来 (SVG)](https://juejin.im/post/585f855961ff4b006ce0f05b)
[SVG与多彩渐变圆环倒计时效果实例页面](http://www.zhangxinxu.com/study/201710/colorful-time-count-down-svg-circle.html)
[如何使用CSS和SVG剪切和遮罩技术](https://segmentfault.com/a/1190000006785931)
[CSS和SVG中的剪切——clip-path属性和<clipPath>元素著作权归作者所有。](https://www.w3cplus.com/css3/css-svg-clipping.html)

[SVG元素上的transform](https://www.w3cplus.com/svg/transforms-on-svg-elements.html)
[超级强大的SVG SMIL animation动画详解](http://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/)
[拥抱Web设计新趋势：SVG Sprites实践应用](https://aotu.io/notes/2016/07/09/SVG-Symbol-component-practice/?o2src=juejin&o2layout=compat)
[将SVG保存为图片](http://www.tangshuang.net/3595.html)
[SVG 应用：Gradient (线性渐变) 在文字中的应用](https://segmentfault.com/a/1190000007426350)

---
# SVG 扬帆起航

## 基础认知

SVG「Scalable Vector Graphics」表示「可缩放矢量图形『放大不模糊』」  
一个基础的 SVG 文档由 `<svg>` 根元素和 [基本形状元素](https://developer.mozilla.org/en-US/docs/Web/SVG/Element) 构成  
作为 XML 的一种方言，SVG 必须正确的绑定命名空间 （在 xmlns 属性中绑定）。[命名空间速成](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Namespaces_Crash_Course) 获取更多信息。
SVG 文件全局有效的规则是 「后来居上」，越后面的元素越可见

### 能做什么

动画、图形、渐变、旋转、滤镜、JavaScript 接口……「各种超酷的动画」

### 和 HTML 使用的几种方式

**`<img src="xxx.svg" height="10" width="10" />`**  
不能使用JS来控制

**`.svg { background-image: url(xxx.svg);}`**  
最好不使用 base64 格式化 SVG「阻塞其它资源」、不能使用 JS 控制

**`<iframe src="xxx.svg">Not support iframe</iframe>`**

**`<embed type="image/svg+xml" src="xxx.svg" />`**

**`<object type="image/svg+xml" data="xxx.svg">Not support SVG</object>`**
能使用JS来控制「推荐方式」

**`<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 10 10">…</svg>`**
节省 HTTP 请求，能使用 JS 控制，不能被浏览器缓存

## CSS、JS 与 SVG

### 内敛样式

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 68 65">
  <style type="text/css">
    <![CDATA[
    .red { strock: #f00; }
    ]]>
  </style>
  <path class="red" d="M10 10v20" />
</svg>
```

### 外链样式

```html
<?xml-stylesheet type="text/css" href="xxx.css"?>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 68 65">
  <path class="cls" d="M42 27v-20" />
</svg>
```

### JS 操作 SVG

如果 SVG 代码作为 DOM 在 HTML 内部，可以向平常一样操作 DOM 操作 SVG  
如果是使用 `<object>` 你可以使用 [contentDocument](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLIFrameElement/contentDocument) 来控制它 SVG

**注意**

1. `<img>`、`background-image` 形式的 SVG 不支持「外链 CSS、JS」  
1. 内敛 CSS 和 JS 最好放在 `<![CDATA[` 与 `]]>` 之中

## `<path />`

别说话，先举个 🌰 ，一起认识一下 path：[点我](https://jsfiddle.net/hangyangws/ek7s4v1d/5/)

> 基于 path 的不同属性，可以画出各种各样的路径，所以 path 可算是 SVG 的「节点之王」  

**命令**  
命令都用一个关键字母来表示，命令 **都有两种** 表示方式

1. 大写字母，表示采用「绝对定位」
1. 小写字母，表示采用「相对定位『相对于上一个点』」

### path 的命令列表

- `M`：moveto 移动到
- `L`：lineto 画线到
- `H`：horizontal lineto 水平线到
- `V`：vertical lineto 垂直线到
- `C`：curveto 三次贝塞尔曲线
- `S`：smooth curveto 光滑三次贝塞尔曲线
- `Q`：quadratic Belzier curve 二次贝塞尔曲线
- `T`：smooth quadratic Belzier curveto 光滑二次贝塞尔曲线
- `A`：elliptical Arc 椭圆弧
- `Z`：closepath 关闭路径

**注意**：Z 命令不区分大小写

### path 的命令详解

- L

L 命令将会在当前位置和新位置之间画一条线段：L x y (or l dx dy)  
还有两个简写命令：H，绘制平行线。V，绘制垂直线。这两个命令都只带一个参数，标明在 x 或 y 轴移动到的位置：`H x (or h dx)` 、`V y (or v dy)`

- Z

Z 命令会从当前点画一条直线到路径的起点，所以它还是经常被放到路径的最后。另外，Z 命令不用区分大小写：Z (or z)

- C

`C x1 y1, x2 y2, x y` 或 `c dx1 dy1, dx2 dy2, dx dy`  
(x1, y1)、(x2, y2) 分别是起点、终点控制点。最后一个坐标 (x, y)，表示曲线的终点  
三次贝塞尔曲线 **表现形式** 是：曲线沿着 **起点开始** 到第一控制点的方向伸出，逐渐弯曲，然后沿着第二控制点到 **终点的方向结束**

- S

S 命令可以用来创建与之前那些曲线一样的贝塞尔曲线，通常和 C 命令一起使用  
如果 S 命令跟在一个 C 命令或者另一个 S 命令的后面，它的第一个控制点，就会被假设成前一个控制点的对称点，不应该写出来，所以 S 省略了一个对称点

- Q

`Q x1 y1, x y` 或 `q dx1 dy1, dx dy`  

- T

`T x y` 或 `t dx dy`  
T 命令类似于 S 命令，用于二次贝塞尔曲线。T 命令前面最好是一个 Q 命令，或者是另一个 T 命令  
如果 T 单独使用，那么控制点就会被认为和终点是同一个点，所以画出来的将是一条直线

- A

`A rx ry x-axis-rotation large-arc-flag sweep-flag x y` 或 `a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy`

rx ry：「椭圆」的 x，y半径  
x-axis-rotation：X 轴旋转角度，顺时针为正数  
large-arc-flag：1 表示用大弧度，0 表示小弧度  
sweep-flag：弧度回话方向，1 顺时针，0 逆时针  
x y：弧度终点

---

## SVG 动画

- SVG 本身的动画「基于 SMIL」「主要借助 SVG `<animate>` 标签」
- CSS3 动画「animation、transition『不是 svg 的重点』」
- JS 动画「DOM 操作『忽视它』」


---

## 贝塞尔曲线

[点我](http://www.cnblogs.com/hnfxs/p/3148483.html)

## `<g>`

用来把若干个基本形状编成一个组

## `<viewBox>`

可以做到放缩的效果

## `<polygon />`

最后一个点会自动和第一个点连接



**d 属性**  
path 元素的形状是通过属性 d 定义的，属性 d 的值是一个「命令 + 参数」的序列

### 填充、边框、样式

常见属性：fill stroke fill-opacity stroke-opacity  
stroke-width：描边宽度，不是路径宽度  
strke-linecap：绘制描边的方式，边框 **终点** 的形状  
stroke-linejoin：控制两条描边线段之间的方式连接  
stroke-dasharray：一组用逗号分割的数字组成的数列 **必须用逗号分**  
*注意：FireFox 3+ 支持 rgba ，但为了在其他浏览器中兼容，最好将 `rgba` 和 `*-opacity` 分开使用，如同时使用，则都将调用*

**使用CSS**
把 background-color、border 改成 fill 和 stroke  
上色和填充的部分一般是可以用CSS来设置的，比如fill，stroke，stroke-dasharray，但不包括渐变和图案等。  
另外，width、height，以及路径的命令等等，都不能用 css 设置  
*不是所有的属性都能用CSS来设置*：[SVG 规范](https://www.w3.org/TR/SVG/propidx.html) 将属性区分成 properties 和 attributes，前者是可以用 CSS 设置的，后者不能

1. 利用style属性插入到元素的行间：`<rect style="stroke: #fff;"/>`
1. 利用 `<style>` 在 html `<head>` 里；在 svg `<defs>` 标签里

`<defs>` 表示定义，这里面可以定义一些不会在 SVG 图形中出现、但是可以被其他元素使用的元素

### 渐变

[link](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Gradients)

### 图案

[link](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Patterns)

### Texts

[link](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Texts)

### 基础变形

[link](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Basic_Transformations)

### 剪切和遮罩

[link](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Clipping_and_masking)

### SVG 字体

[link](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/SVG_fonts)

### 嵌入到 HTML 文件

- 如果HTML是XHTML并且声明类型为application/xhtml+xml，可以直接把SVG嵌入到XML源码中。
- 如果HTML是HTML5并且浏览器支持HTML5，同样可以直接嵌入SVG。然而为了符合HTML5标准，可能需要做一些语法调整。
- 可以通过 object 元素引用SVG文件
- 类似的也可以使用 iframe 元素引用SVG文件
- 理论上同样可以使用 img 元素，但是在低于4.0版本的Firefox 中不起作用。
- 最后SVG可以通过JavaScript动态创建并注入到HTML DOM中。 这样具有一个优点，可以对浏览器使用替代技术，在不能解析SVG的情况下，可以替换创建的内容。

### Notes

- SVG 里的属性值必须用引号引起来，就算是数值也必须这样做
- SVG 的元素和属性必须按标准格式书写，因为 XML 是区分大小写的「这一点和 HTML 不同」
- SVG 元素可以用 CSS 的 fill 填充颜色：`path { fill: currentColor; }`
