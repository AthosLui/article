# word-break、word-wrap、overflow-wrap 和 white-space运用与差别

一些前端开发对这三个属性有一定的「困惑」，接下来对他们进行简单的解释与区别

### word-break

顾名思义，`word-break` 指定了怎样在单词内断行

**常用的值**：

- normal

「中文/日文/韩文」会自动换行，「连续的数字和英文之间」不会自动换行

- break-all

在任意字符之间换行，包括「连续的数字和英文」

- keep-all

「连续的中文/日文/韩文/英文/数字」不会自动换行

**注意**：

不论是「中文/日文/韩文」还是「英文/数字」，都会「连续」和「非连续」状态，  
比如：「我是连续中文」、「我 是 非 连 续 中 文」  
首先记住一点「任何语言，只要是非连续的，都会换行」  
还要记住一点，在一些浏览器中「例如：Chrome」支持 `break-word` 值，但是 `break-word` 不是官网属性，最好不要使用

### word-wrap、overflow-wrap

**注意**：

`word-wrap` 属性原本属于微软的一个私有属性，在 CSS3 现在的文本规范草案中已经被重名为 `overflow-wrap`  
`word-wrap` 现在被当作 `overflow-wrap` 的 「别名」  
稳定的谷歌 Chrome 和 Opera 浏览器版本支持这种新语法

**常用的值**：

- break-word

如果元素没有多余的地方容纳该单词到结尾，则单词会被强制分割换行

### white-space

`white-space` 告诉浏览器何处理元素中的空白符

**常用的值**：

- normal

「默认」忽略空白符，忽略原有换行符，自动换行

- nowrap

忽略空白符，文本不换行，直到遇到 `</br>` 标签才换行

- pre

保留空白符，保留换行符，即保留原有格式，不会自动换行  
用户从 `<textarea>` 输入内容，如果把内容放在普通标签里面，则会丢失换行符，`pre` 属性可以保持换行符

- pre-wrap

保留空白符、换行符，自动进行换行

- pre-line

合并空白符，保留换行符

# CSS inline

# 盒模型之：W3C 与 IE 的区别

# flex 的使用

# CSS hack 技术

# margin 重叠现象与 BFC

BFC 是 css 布局的一个概念，代表一块区域或者一个环境，是一个独立的渲染区域  
我们常说的文档流其实分为「定位流、浮动流、普通流」三种，BFC 中的 FC 指的就是「普通流」  
FC 是 formatting context 的首字母缩写，直译为「格式化上下文」  
FC 是页面中的一块渲染区域，有一套自己渲染规则，决定了其子元素如何布局，以及和其他元素之间的关系和作用  

下列条件之一就可触发 BFC

1. 根元素，即 HTML 元素
2. float 的值不为 none
3. overflow 的值不为 visible
4. display 的值为 inline-block、table-cell、table-captio
5. position 的值为 absolute 或 fixed

[link](https://juejin.im/post/5909db2fda2f60005d2093db)

# line-height 以及 vertical-align

无单位的line-height 是 font-size相关联的  
但问题是font-size：100px在不同字体时表现是不一样的

[link](http://web.jobbole.com/91180/)
