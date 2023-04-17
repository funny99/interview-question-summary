# 从浏览器地址栏输入url到显示页面的步骤 
## 基础版本
- 浏览器根据请求的 URL 交给 DNS 域名解析，找到真实 IP ， 向服务器发起请求;
- 服务器交给后台处理完成后返回数据， 浏览器接收文件 ( HTML、JS、CSS 、图象等); 
- 浏览器对加载到的资源 ( HTML、JS、CSS 等) 进行语法解析， 建立相应的内部数据结构
( 如HTML 的DOM ); 
- 载入解析到的资源文件， 渲染页面， 完成。
## 详细版
1. 在浏览器地址栏输入URL
2. 浏览器查看缓存:
    1. 如果资源未缓存，发起新请求
    2. 如果已缓存，检验是否足够新鲜， 足够新鲜直接提供给客户端， 否则与服务器进行验 证。
    3. 检验新鲜通常有两个HTTP头进行控制 Expires 和 Cache-Control : HTTP1.0提供Expires，值为一个绝对时间表示缓存新鲜日期 HTTP1.1增加了Cache-Control: max-age=,值为以秒为单位的最大新鲜时间
3. 浏览器解析URL获取协议， 主机，端口， path
4. 浏览器组装一个HTTP ( GET) 请求报文 
5. 浏览器获取主机ip地址， 过程如下:
    1. 浏览器缓存
    2. 本机缓存
    3. hosts文件
    4. 路由器缓存
    5. ISP DNS缓存
    6. DNS递归查询 ( 可能存在负载均衡导致每次IP不一样)
6. 打开一个socket与目标IP地址，端口建立TCP链接，三次握手如下:       
    1. 客户端发送一个TCP的SYN=1，Seq=X的包到服务器端口
    2. 服务器发回SYN=1， ACK=X+1， Seq=Y的响应包
    3. 客户端发送ACK=Y+1， Seq=Z
7. TCP链接建立后发送HTTP请求
8. 服务器接受请求并解析，将请求转发到服务程序
9. 服务器检查HTTP请求头是否包含缓存验证信息如果验证缓存新鲜， 返回304等对应状态码 
10. 处理程序读取完整请求并准备HTTP响应， 可能需要查询数据库等操作
11. 服务器将响应报文通过TCP连接发送回浏览器
12. 浏览器接收HTTP响应，然后根据情况选择关闭TCP连接或者保留重用，关闭TCP连接的四 次握手如下:
    1. 主动方发送Fin=1， Ack=Z， Seq=X报文 
    2. 被动方发送ACK=X+1， Seq=Z报文 
    3. 被动方发送Fin=1， ACK=X， Seq=Y报文 
    4. 主动方发送ACK=Y， Seq=X报文
13. 浏览器检查响应状态码:是否为1XX， 3XX， 4XX， 5XX， 这些情况处理与2XX不同 
14. 如果资源可缓存， 进行缓存
15. 对响应进行解码 (例如gzip压缩)
16. 根据资源类型决定如何处理 (假设资源为HTML文档)
17. 解析HTML文档，构件DOM树，下载资源，构造CSSOM树，执行js脚本， 这些操作没有严 格的先后顺序， 以下分别解释
18. 构建DOM树:
    1. Tokenizing:根据HTML规范将字符流解析为标记
    2. Lexing:词法分析将标记转换为对象并定义属性和规则
    3. DOM construction:根据HTML标记关系将对象组成DOM树 
19. 解析过程中遇到图片 、样式表 、js文件，启动下载
20. 构建CSSOM树:
    1. Tokenizing:字符流转换为标记流
    2. Node:根据标记创建节点
    3. CSSOM:节点创建CSSOM树
21. 根据DOM树和CSSOM树构建渲染树:
    1. 从DOM树的根节点遍历所有可见节点，不可⻅节点包括:1) 不可⻅的标签。2)被css隐藏的节点， 如display:none
    2. 对每一个可⻅节点，找到恰当的CSSOM规则并应用
    3. 发布可视节点的内容和计算样式
22. js解析如下:
    1. 浏览器创建Document对象并解析HTML，将解析到的元素和文本节点添加到文档中，此 时document.readystate为loading
    2. HTML解析器遇到没有async和defer的script时，将他们添加到文档中，然后执行行内 或外部脚本 。这些脚本会同步执行， 并且在脚本下载和执行时解析器会暂停 。这样就可 以用document.write()把文本插入到输入流中 。同步脚本经常简单定义函数和注册事件 处理程序，他们可以遍历和操作script和他们之前的文档内容
    3. 当解析器遇到设置了async属性的script时， 开始下载脚本并继续解析文档 。脚本会在它 下载完成后尽快执行，但是解析器不会停下来等它下载 。异步脚本禁止使用 document.write()， 它们可以访问自己script和之前的文档元素
    4. 当文档完成解析，document.readState变成interactive 
    5. 所有defer脚本会按照在文档出现的顺序执行，延迟脚本能访问完整文档树， 禁止使用document.write()
    6. 浏览器在Document对象上触发DOMContentLoaded事件
    7. 此时文档完全解析完成， 浏览器可能还在等待如图片等内容加载， 等这些内容完成载入 并且所有异步脚本完成载入和执行，document.readState变为complete，window触发 load事件
23. 显示页面 ( HTML解析过程中会逐步显示页面) 
## 详细简版
1. 从浏览器接收 url 到开启网络请求线程 ( 这一部分可以展开浏览器的机制以及进程与线程 之间的关系)
2. 开启网络线程到发出一个完整的 HTTP 请求 ( 这一部分涉及到dns查询， TCP/IP 请求， 五层因特网协议栈等知识)
3. 从服务器接收到请求到对应后台接收到请求 (这一部分可能涉及到负载均衡， 安全拦截以 及后台内部的处理等等)
4. 后台和前台的 HTTP 交互 ( 这一部分包括 HTTP 头部 、响应码 、报文结构 、 cookie 等知 识， 可以提下静态资源的 cookie 优化， 以及编码解码， 如 gzip 压缩等)
5. 单独拎出来的缓存问题， HTTP 的缓存 ( 这部分包括http缓存头部， ETag ， catch-
control 等)
6. 浏览器接收到 HTTP 数据包后的解析流程 ( 解析 html -词法分析然后解析成 dom 树 、解 析css生成css规则树、合并成render树，然后layout、 painting渲染、复合图 层的合成 、 GPU 绘制 、外链资源的处理 、 loaded 和 DOMContentLoaded 等)
7. CSS 的可视化格式模型 ( 元素的渲染规则， 如包含块，控制框， BFC ， IFC 等概念) 
8. JS 引擎解析过程 ( JS 的解释阶段，预处理阶段，执行阶段生成执行上下文， VO ，作用域链 、回收机制等等)
9. 其它 ( 可以拓展不同的知识模块， 如跨域，web安全， hybrid 模式等等内容)

> [从输入 URL 到页面展示到底发生了什么？看完吊打面试官！](https://zhuanlan.zhihu.com/p/133906695)

# 浏览器内核
主要分成两部分:渲染引擎( layout engineer 或 Rendering Engine )和 JS 引擎
渲染引擎:负责取得网页的内容 ( HTML 、 XML 、图像等等) 、整理讯息 (例如加入
CSS 等)， 以及计算网页的显示方式，然后会输出至显示器或打印机 。浏览器的内核的不 同对于网页的语法解释会有不同，所以渲染的效果也不相同 。所有网页浏览器 、电子邮件 客户端以及其它需要编辑 、显示网络内容的应用程序都需要内核
JS 引擎则:解析和执行 javascript 来实现网页的动态效果
最开始渲染引擎和 JS 引擎并没有区分的很明确，后来JS引擎越来越独立， 内核就倾向于只指渲染引擎

# cookies ， sessionStorage 和 localStorage 的区别?
- cookie 是网站为了标示用户身份而储存在用户本地终端 ( Client Side)上的数据 ( 通常
经过加密)
- cookie数据始终在同源的http请求中携带 ( 即使不需要)， 即会在浏览器和服务器间来回传递。
sessionStorage 和 localStorage 不会自动把数据发给服务器，仅在本地保存 
- 存储大小:
    - cookie 数据大小不能超过4k
    - sessionStorage 和 localStorage 虽然也有存储大小的限制，但比 cookie 大得 多， 可以达到5M或更大
- 有效期:
    - localStorage 存储持久数据， 浏览器关闭后数据不丢失除非主动删除数据
    - sessionStorage 数据在当前浏览器窗口关闭后自动删除
    - cookie 设置的 cookie 过期时间之前一直有效， 即使窗口或浏览器关闭

> [sessionStorage 、localStorage 和 cookie 之间的区别](https://juejin.cn/post/6844903713098694664)