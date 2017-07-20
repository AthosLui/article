# SVG 出发啦

[link for w3cPlus](https://www.w3cplus.com/blog/tags/411.html?page=2)

### 基础知识

SVG「Scalable Vector Graphics」表示「可缩放矢量图形」，和 HTML 面向文本相比较，SVG 面向图形  
一个简单的 SVG 文档由 `<svg>` 根元素和 [基本的形状元素](https://developer.mozilla.org/en-US/docs/Web/SVG/Element) 构成

g 元素，它用来把若干个基本形状编成一个组
SVG 支持渐变、旋转、滤镜效果、JavaScript 接口等等功能
属性 version 和属性 baseProfile 属性是必不可少的，供其它类型的验证方式确定 SVG 版本
作为 XML 的一种方言，SVG 必须正确的绑定命名空间 （在 xmlns 属性中绑定）。请阅读 [命名空间速成](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Namespaces_Crash_Course) 获取更多信息

SVG文件全局有效的规则是“后来居上”，越后面的元素越可见

viewBox 可以做到放缩的效果

`<polygon />` 的最后一个点会自动和第一个点连接

### `<path />` 节点

**d 属性**  
path 元素的形状是通过属性 d 定义的，属性 d 的值是一个「命令 + 参数」的序列

**命令**  
每一个命令都用一个关键字母来表示，比如，字母「M」表示的是「Move to」命令  
每一个命令都有两种表示方式，一种是用大写字母，表示采用绝对定位。另一种是用小写字母，表示采用相对定位「相对于上一个点」。Z 命令不区分大小写

**L 命令**  
L 命令将会在当前位置和新位置之间画一条线段：L x y (or l dx dy)  
还有两个简写命令：H，绘制平行线。V，绘制垂直线。这两个命令都只带一个参数，标明在 x 或 y 轴移动到的位置：`H x (or h dx)` 、`V y (or v dy)`

**Z 命令**  
Z 命令会从当前点画一条直线到路径的起点，但是它还是经常被放到路径的最后。另外，Z 命令不用区分大小写：Z (or z)

**三次贝塞尔曲线 C**
`C x1 y1, x2 y2, x y` 或 `c dx1 dy1, dx2 dy2, dx dy`  
(x1, y1)、(x2, y2) 分别是起点、终点控制点。最后一个坐标 (x, y)，表示曲线的终点  
三次贝塞尔曲线 **表现形式** 是：曲线沿着 **起点开始** 到第一控制点的方向伸出，逐渐弯曲，然后沿着第二控制点到 **终点的方向结束**

**S 命令**  
S 命令可以用来创建与之前那些曲线一样的贝塞尔曲线，通常和 C 命令一起使用  
如果 S 命令跟在一个 C 命令或者另一个 S 命令的后面，它的第一个控制点，就会被假设成前一个控制点的对称点，不应该写出来，所以 S 省略了一个对称点

**二次贝塞尔曲线 Q**
`Q x1 y1, x y` 或 `q dx1 dy1, dx dy`  

**T 命令**  
`T x y` 或 `t dx dy`  
T 命令类似于 S 命令，用于二次贝塞尔曲线。T 命令前面最好是一个 Q 命令，或者是另一个 T 命令  
如果 T 单独使用，那么控制点就会被认为和终点是同一个点，所以画出来的将是一条直线

**A 命令**  

`A rx ry x-axis-rotation large-arc-flag sweep-flag x y` 或 `a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy`

rx ry：「椭圆」的 x，y半径  
x-axis-rotation：X 轴旋转角度，顺时针为正数  
large-arc-flag：1 表示用大弧度，0 表示小弧度  
sweep-flag：弧度回话方向，1 顺时针，0 逆时针  
x y：弧度终点

### 填充和边框与样式

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
