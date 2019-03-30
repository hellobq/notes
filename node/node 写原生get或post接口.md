# node 写原生get或post接口

通过 `req.method` 分别是 `GET` / `POST` 接口。

对于 `GET`，拿到参数的方式有：

- 使用 node 内部模块 `url` 解析 `req.url`;
- 使用正则 /(\w+)=(\w+)/g;

对于 `POST`，拿到参数的方式有：

- 对于字符串的参数，使用 node 内部模块 `querystring.parse()` 模块编译并格式化参数即可。
- 对于二进制文件。需要使用 Buffer 类处理。例如：文件上传。

## demo

    const http = require('http')
    const fs = require('fs')
    const Url = require('url')
    const querystring = require('querystring')

    const server = http.createServer((req, res) => {
      const { method, url } = req

      if (method === 'GET') {
        const data = Url.parse(url, true).query
        // ...
        res.statusCode = 200
        res.end(JSON.stringify({
          success: true
        }))
      }

      if (method === 'POST') {
        let buffers = [], data = null

        req.on('data', chunk => {
          buffers.push(chunk) 
        })

        req.on('end', () => {
          const buffer = Buffer.concat(buffers)

          // 如果是文件上传，chunk 就是二进制数据，需要使用二进制类 Buffer 处理数据
          data = querystring.parse(buffer.toString())
          console.log(data)
        })

        res.writeHead(200)
        res.end(
          JSON.stringify({
            success: true
          })
        )
      }
    })

    server.listen('3000', () => console.log('server start at 3000!'))
