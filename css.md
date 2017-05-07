# word-break、word-wrap 和 white-space运用与差别

### white-space

告诉浏览器何处理元素中的空白符  
可能的值：  
**normal**：默认，忽略空白符，忽略原有换行符。自动换行，不会有滚动条  
**pre**：保留空白符；保留换行符，即保留原有格式  
**nowrap**：忽略空白符，文本不换行，直到遇到</br>  
**pre-wrap**：保留空白符，自动进行换行，不会有滚动条  
**pre-line**：合并空白符，保留换行符

### word-wrap

### word-break

# CSS inline

# 盒模型(W3C和IE)

# flex的使用

# CSS hack技术

# margin重叠现象与BFC

所谓的BFC就是css布局的一个概念，是一块区域，一个环境  
是一个独立的渲染区域  
我们常说的文档流其实分为定位流、浮动流和普通流三种。而普通流其实就是指BFC中的FC  
FC是formatting context的首字母缩写，直译过来是格式化上下文，它是页面中的一块渲染区域，有一套渲染规则，决定了其子元素如何布局，以及和其他元素之间的关系和作用  
下列条件之一就可触发BFC

1. 根元素，即HTML元
2. float的值不为non
3. overflow的值不为visibl
4. display的值为inline-block、table-cell、table-captio
5. position的值为absolute或fixed

[link](https://juejin.im/post/5909db2fda2f60005d2093db)

# line-height 以及 vertical-align

无单位的line-height 是 font-size相关联的  
但问题是font-size：100px在不同字体时表现是不一样的

[link](http://web.jobbole.com/91180/)
