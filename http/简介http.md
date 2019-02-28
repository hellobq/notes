# http

建立在TCP（网络层）连接的应用层协议。

## http 特点

- 请求简单。对于**get**请求，最简只需要一个**url**即可。
- 灵活。通过http协议可以传输各种类型数据，由字段**Content-Type/Accept-Type**标注。
- 无连接。每次连接只能处理一次请求，处理完成后立即断开。可以连续地请求和响应，因为设置了长连接。
- 无状态。http协议对事务处理没有记忆功能。不能区分用户的身份，否则也不会出现session和**cookie**。

## http版本

#### http0.9 单行协议

- request只有**GET**请求和请求的**url**，response只有HTML文档的主体部分。
- 没有头部信息，不包含状态码。

#### http1.0 增加扩展性

- 协议版本信息在请求行上表明，如：**HTTP/1.0**。
- 有头部信息，有了状态码。
- 因为有了**Content-Type**，可以传输除HTML文档外的数据。

#### http1.1 标准化的协议

- 可实现长连接，节省每次TCP建立连接的时间。
- 引入缓存机制。
- 引入了数据协商机制（包括：语言、编码、类型）等。
...

#### http2.0 更优异的协议

- 不再是http1.1一样的文本协议，而是二进制协议。因为数据的传输是使用二进制。
- 压缩了headers，对UA、Cookie等信息都有压缩。减少带宽。
- 同一个TCP链接的多个Http请求不再是顺序执行的，可以并发请求。
- 服务器推送，允许服务器向客户端的缓存中存放数据。
...

## http报文的组成部分

- 请求行：method、url、HTTP/版本号
- 请求头：各种键值对儿。
- 空行。\n\r这种转义字符组成，为了把请求头和请求体分开，让服务器分别解析。
- 请求体：向服务器发送的请求参数。

- 响应头：HTTP/版本号 状态码（status_code） 状态信息（status_message）
- 响应头
- 空行
- 请求体。服务器返回的资源。

## HTTP 请求方法

GET 获取数据
HEAD 仅获得报文头部
POST 传输资源
PUT 更新资源
DELETE 删除指定资源
OPTIONS 发送预请求，确认服务器是否允许客户端发送这种请求。

## CORS

因为同源策略的限制，例如Ajax/Fetch API是实现跨域的HTTP请求结果被浏览器拦截。跨域资源共享 CORS。它使得上述需求得以实现。

#### 具体的实现原理

通过在响应头部增加一些额外的、以**Access-Control-Allow-..**开头的headers，允许服务器声明哪些站点通过浏览器可以访问得到资源。

``` js
// 请求发出点
origin: 和跨域无关

// 允许哪些站点可跨域请求
Access-Control-Allow-Origin

// CORS预请求中使用 PUT OPTIONS方法
Access-Control-Allow-Method: PUT, OPTIONS

// CORS预请求中，携带的头部
Access-Control-Allow-Headers: X-PINGOTHER

// 一段时间内，不再需要发送CORS预请求
Access-Control-Max-Age: 86400
```

## OPTIONS 请求方式

除了简单请求以外的请求在发送之前都需要执行预请求（OPTIONS）。预请求：征求服务器的同意，是否可以使用其他的methods、headers

#### 以下请求可视为简单请求

方法仅限于：GET、POST、HAED

请求头仅限于：Accept、Accept-Language、Content-Language、Content-Type（仅限于：text/plain、multipart/form-data、application/x-www-form-urlencoded）

