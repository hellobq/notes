# http

[http](http://nodejs.cn/api/http.html#http_http) 是node的内置模块，负责基于 http 协议的前后台通讯服务。http模块内置多个类，每个类封装了各种方法。

## node 服务 demo

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

[http.server](http://nodejs.cn/api/http.html#http_class_http_server)类继承 net.server （负责创建TCP）这个类，举例一下语法：

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

[http.ServerResponse](http://nodejs.cn/api/http.html#http_class_http_serverresponse) 是由服务器创建的响应对象（可写流），在 [request](http://nodejs.cn/api/http.html#http_event_request) 事件中，位于第二个参数。用来响应服务。

    // 设置响应头
    res.setHeader(key<string>, value<any>)
    res.setHeader('name', 'hhaha')
    res.setHeader('Set-Cookie', ['type=ninja', 'language=javascript'])

    // 还能通过 writeHead 设置响应头
    res.writeHead(statusCode<number>[, statusMessage][, headers])
    res.writeHead(200, {
      'name': 'haha',
      'Set-Cookie': ['language=javascript', 'type=ninja']
    })

    /*
      区别：
        setHeader 可以调用多次，writeHead 只能调用一次。
        setHeader 设置的响应头和 writeHead 设置的响应头会合并，相同 key 的头部将会覆盖。
        writeHead 可以传输状态码，setHeader 需要使用 statusCode。
    */

    // res.end(data)表示服务端数据处理完成、结束响应流，并向客户端发送了信息data（可选）
    res.end(
      [data <string|Buffer> ] 
      [, encoding <string> ]
      [, callback <Function> ]
    )
    
    /* 
      也可以使用 res.write() 返回内容，但是必须显示调用 res.end()，否则前端一直 waiting。

      res.write(
        chunk<string | Buffer>
        [, encoding<string = 'utf8'>]
        [, callback<function>]
      )

      如果 res.end() 也有返回的内容，会自动和 res.write() 中的 chunk 拼接。
    */
