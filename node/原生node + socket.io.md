# 原生node + socket.io

基于 `webscoket` 封装的库。解决 `webscoket` 兼容问题。以下代码是个 demo，前后台使用 [scoket.io](https://github.com/socketio/socket.io) 全双工库，用原生 node 创建服务。

``` js
// index.js
const http = require('http')
const fs = require('fs')
const io = require('socket.io')
const port = process.env.PORT || 3000;

const server = http.createServer((req, res) => {
  const { method, url } = req
  if (method.toUpperCase() === 'GET' && url === '/') {
    fs.readFile(__dirname + '/index.html', { encoding: 'utf8' }, (err, data) => {
      if (err) {
        console.log('文件不存在...', err)
      }
      res.writeHead(200, {
        'Content-Type': 'text/html'
      })
      res.end(data)
    })
  }
})

const ws = io(server)
ws.on('connection', (server) => {
  // 触发 msg 事件
  server.emit('msg', '服务端向客户端发送数据第一条', '服务端向客户端发送数据第二条')

  // 监听来自 client 的 msg 事件
  server.on('msg', (...msgs) => {
    console.log(msgs)   // ['客户端向服务端发送数据第一条', '客户端向服务端发送数据第二条']
  })
})

server.listen(port, () => console.log(`server start at ${port}`))
```

``` html
// index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <p>哈哈哈</p>
  <script src="http://localhost:3000/socket.io/socket.io.js"></script>
  <script>
    const socket = io.connect('ws://localhost:3000/');

    // 触发 msg 事件
    socket.emit('msg', '客户端向服务端发送数据第一条', '客户端向服务端发送数据第二条')

    // 监听来自 server 的 msg 事件
    socket.on('msg', (...msgs) => {
      console.log(msgs)   // ['服务端向客户端发送数据第一条', '服务端向客户端发送数据第二条']
    })
  </script>
</body>
</html>
```

学习链接：
- [官方例子：express + scoket.io](https://github.com/socketio/socket.io/tree/master/examples/chat)
- [scoket.io](https://www.jianshu.com/p/4e80b931cdea)
- [scoket.io 官网](https://socket.io/get-started/chat/#Getting-this-example)
