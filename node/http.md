# http

[http](http://nodejs.cn/api/http.html#http_http) 是node的内置模块，负责前后台通讯服务。http模块内置多个类，每个类封装了各种方法。

## demo

新建一个http服务，当用户访问localhost:3000时，返回'hello node'。

``` js
const http = require('http')

const server = http.createServer((req, res) => {
  if (req.url === '/') {
    res.end('hello node')
  }
})

server.listen(3000, () => console.log('server start at 3000!'))

```

## http.server类

[http.server](http://nodejs.cn/api/http.html#http_class_http_server)类继承net.server（负责创建TCP）这个类，举例一下语法：

``` js
// 监听server close事件
server.on('close', () => {
  // ,,,
})

// server启动成功后，server的监听将会触发
server.listen(3000, () => console.log('server start at 3000!'))

```

## http.IncomingMessage类

[http.IncomingMessage](http://nodejs.cn/api/http.html#http_class_http_incomingmessage) 实例（可读流）用来获取请求消息头和数据。

req.url: 请求地址

req.httpVersion: http版本

req.headers: 请求头

req.method: 请求方法

## http.ServerResponse类

[http.ServerResponse](http://nodejs.cn/api/http.html#http_class_http_serverresponse)是由服务器创建的响应对象（可写流），在[“request”](http://nodejs.cn/api/http.html#http_event_request)事件中，位于第二个参数。用来相应服务，设置响应头等。

``` js
// 设置响应头
res.setHeader(key<string>, value<any>)
res.setHeader('name', 'hhaha')
res.setHeader('Set-Cookie', ['type=ninja', 'language=javascript'])

// 还能通过 writeHead设置响应头
res.writeHead(statusCode<number>[, statusMessage][, headers])
res.writeHead(200, {
  'name': 'haha',
  'Set-Cookie': ['language=javascript', 'type=ninja']
})

/*
  区别：
    setHeader可以调用多次，writeHead只能调用一次。
    setHeader设置的响应头和writeHead设置的响应头会合并，相同key的头部将会覆盖。
    writeHead可以传输状态码，setHeader就不行。
*/


// res.end(opts)表示服务端数据处理完成，并向request发送了信息data（可选）

res.end(
  [data <string|Buffer> ] 
  [, encoding <string> ]
  [, callback <Function> ]
) 
```
