# HTTP的几种请求方法用途 
- `GET`方法
GET 方法请求一个指定资源的表示形式，使用 GET 的请求应该只被用于获取数据。
- `POST`方法
向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改。
- `PUT`方法
PUT 用请求体 payload 中的数据替换整个资源。如果没有与请求体唯一标识相匹配的资源，它将创建一个新资源。
- `PATCH`方法
是对 PUT 方法的补充，用来对已知资源进行局部更新 。
- `HEAD`方法
类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头
- `DELETE`方法
DELETE 方法删除指定的资源。
- `OPTIONS`方法
用于获取目的资源所支持的通信选项。客户端可以对特定的 URL 使用 OPTIONS 方法，也可以对整站（通过将 URL 设置为“*”）使用该方法。
- `TRACE`方法
HTTP TRACE 方法 实现沿通向目标资源的路径的消息环回（loop-back）测试，提供了一种实用的 debug 机制。
- `CONNECT`方法
在 HTTP 协议中，CONNECT 方法可以开启一个客户端与所请求资源之间的双向沟通的通道。它可以用来创建隧道（tunnel）。

HTTP/1.1协议中共定义了八种方法（有时也叫“动作”），来表明Request-URL指定的资源不同的操作方式
HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法。
HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法

> [OPTIONS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS)

> [常见的HTTP Method深度解析](https://segmentfault.com/a/1190000013182974)