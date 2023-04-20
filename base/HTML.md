# HTML 语义化？
- 让人更容易读懂（增加代码可读性）。
- 让搜索引擎更容易读懂，有助于爬虫抓取更多的有效信息，爬虫依赖于标签来确定上下文和各个关键字的权重（SEO）。
- 在没有 CSS 样式下，页面也能呈现出很好地内容结构、代码结构。

# 前端需要注意哪些SEO
- 合理的`title`、`description`、`keywords`:  
搜索对这三项的权重逐个减小， `title`值强调重点即可， 重要关键词出现不要超过2次， 而且要靠前，不同⻚面`title`要有所不同; `description`把⻚面内容高度概括， ⻓度合适，不可过分堆砌关键词，不同⻚面`description`有所不同; `keywords` 列举出重要关键词即可
- 语义化的`HTML`代码，符合W3C规范: 
语义化代码让搜索引擎容易理解网⻚
- 重要内容`HTML`代码放在最前:
搜索引擎抓取`HTML`顺序是从上到下， 有的搜索引擎对抓取⻓度有限制，保证重要内容一定会被抓取
- 重要内容不要用`js`输出:
爬虫不会执行js获取内容 
- 少用 iframe :
搜索引擎不会抓取`iframe`中的内容
- 非装饰性图片必须加`alt`
- 提高网站速度: 
网站速度是搜索引擎排序的一个重要指标

# \<img\> 的 title 和 alt 有什么区别 
- title: 通常当鼠标滑动到元素上的时候显示
- alt 是\<img\>的特有属性， 是图片内容的等价描述，用于图片无法加载时显示 、读屏器阅读图片 。可提g高图片可访问性， 除了纯装饰图片外都必须设置有意义的值， 搜索引擎会重点分析。

# HTML5
- 增加新特性：
    - 绘画 canvas
    - 用于媒介回放的 video 和 audio 元素
    - 本地离线存储 localStorage 长期存储数据， 浏览器关闭后数据不丢失 sessionStorage 的数据在浏览器关闭后自动删除
    - 语意化更好的内容元素， 比如 article 、 footer 、 header 、 nav 、 section 表单控件， calendar 、 date 、 time 、 email 、 url 、 search
    - 新的技术 webworker 、 websocket 、 Geolocation 
- 移除的元素:
    - 纯表现的元素: basefont、 big、 center、 font、 s、 strike、 tt、u 
    - 对可用性产生负面影响的元素: frame 、 frameset 、 noframes

> [HTML5](https://www.runoob.com/html/html5-intro.html)

# HTML5离线缓存
> [HTML5-离线缓存（Application Cache）](https://juejin.cn/post/6844903590062997517)

# iframe有那些缺点?
- iframe 会阻塞主⻚面的 Onload 事件
- 搜索引擎的检索程序无法解读这种⻚面，不利于 SEO
iframe 和主⻚面共享连接池， 而浏览器对相同域的连接有限制，所以会影响⻚面的并行 加载
- 使用 iframe 之前需要考虑这两个缺点 。如果需要使用 iframe ， 最好是通过 javascript 动态给 iframe 添加 src 属性值， 这样可以绕开以上两个问题

# DOCTYPE
doctype是一种标准通用标记语言的文档类型声明，目的是告诉标准通用标记语言解析器要使用什么样的文档类型定义（DTD）来解析文档。

> [doctype的作用](https://zhuanlan.zhihu.com/p/32609899)

# 行内元素有哪些?块级元素有哪些? 空(void)元素有那些?行内元素和块级元素有什么区别?
- 行内元素有: a b span img input select strong
- 块级元素有: div ul ol li dl dt dd h1 h2 h3 h4... p 
- 空元素: \<br\> \<hr\> \<img\> \<input\> \<link\> \<meta\> 
- 行内元素不可以设置宽高，不独占一行 
- 块级元素可以设置宽高， 独占一行

> [HTML 元素类型](https://zhuanlan.zhihu.com/p/97755100)

# HTML全局属性(global attribute)有哪些
全局属性是所有 HTML 元素共有的属性；它们可以用于所有元素，即使属性可能对某些元素不起作用。
- class :为元素设置类标识 
- data-* : 为元素增加自定义属性 
- draggable : 设置元素是否可拖拽 
- id : 元素 id ，文档内唯一
- lang : 元素内容的的语言
- style : 行内 css 样式
- title : 元素相关的建议信息

>[全局属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes)

# Canvas和SVG有什么区别?
- svg 绘制出来的每一个图形的元素都是独立的 DOM 节点， 能够方便的绑定事件或用来修 改。 canvas输出的是一整幅画布
- svg 输出的图形是矢量图形，后期可以修改参数来自由放大缩小，不会失真和锯齿 。而
canvas 输出标量画布，就像一张图片一样，放大会失真或者锯齿

# HTML5 为什么只需要写 \<!DOCTYPE HTML\>
- HTML5 不基于 SGML ， 因此不需要对 DTD 进行引用，但是需要 doctype 来规范浏览器 的行为
- 而 HTML4.01 基于 SGML ,所以需要对 DTD 进行引用， 才能告知浏览器文档所使用的文档 类型

# 如何在页面上实现一个圆形的可点击区域?
- svg
- border-radius
- 纯 js 实现 需要求一个点在不在圆上简单算法 、获取鼠标坐标等等
- 通过map加area

> [如何在页面上实现一个圆形的可点击区域](https://zhuanlan.zhihu.com/p/48168812)