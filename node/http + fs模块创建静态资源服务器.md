# http + fs模块创建静态资源服务器

文件目录如下：
    
    .
    |-- a.js
    |-- avatar.7s92.jpg
    |-- demo.js (服务器入口文件)
    |-- favicon.ico
    `-- index.html

    0 directories, 5 files

当访问 / 时，返回 index.html，访问其他静态资源时，返回对应的资源。

```js
// demo.js

const http = require('http')
const fs = require('fs')

const server = http.createServer(async (req, res) => {
  if (req.url === '/') {
    fs.readFile(__dirname + '/index.html', { encoding: 'utf8' }, (err, data) => {
      if (err) {
        console.log('文件不存在...', err)
        res.writeHead(404, 'no found', {
          'Content-Type': 'text/html'
        })
        res.end()
      }
      res.writeHead(200, {
        'Content-Type': 'text/html'
      })
      res.end(data)
    })
  }

  if (req.url === '/b.js') {
    fs.readFile(__dirname + '/b.js', { encoding: 'utf8' }, (err, data) => {
      if (err) {
        console.log('文件不存在...', err)
        res.writeHead(404, 'no found', {
          'Content-Type': 'application/javascript'
        })
        res.end()
      }
      res.writeHead(200, {
        'Content-Type': 'application/javascript'
      })
      res.end(data)
    })
  }

  if (req.url === '/avatar.7s92.jpg') {
    fs.readFile(__dirname + '/avatar.7s92.jpg', (err, data) => {
      if (err) {
        console.log('文件不存在...', err)
        res.writeHead(404, 'no found', {
          'Content-Type': 'image/jpg'
        })
        res.end()
      }
      res.writeHead(200, {
        'Content-Type': 'image/jpg'
      })
      res.end(data)
    })
  }

  if (req.url === '/favicon.ico') {
    fs.readFile(__dirname + '/favicon.ico', (err, data) => {
      if (err) {
        console.log('文件不存在...', err)
        res.writeHead(404, 'no found', {
          'Content-Type': 'image/x-icon'
        })
        res.end()
      }
      res.writeHead(200, {
        'Content-Type': 'image/x-icon'
      })
      res.end(data)
    })
  }
})

server.listen('3000', () => console.log('server start at 3000!'))
```
