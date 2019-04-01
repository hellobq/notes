# fetch + node 实现文件上传

文件上传可以是 form 表单，异步上传 fetch 也行。

前端使用 fetch + FormData 传递表单数据，后台 node 使用 [formidable](https://github.com/felixge/node-formidable) 库来解析请求体。

``` html
<input type="file" multiple>
```

``` js
const handlechange = ({target: {files}}) => {
  const formData = new FormData()

  // 添加额外表单数据
  formData.append("username", "Groucho");
  formData.append("accountnum", 123456);
  Array.from(files).forEach((file, idx) => {
    formData.append(idx, file)
  })

  fetch('http://localhost:3000/upload', {
    method: 'POST',
    body: formData
  })
    .then(res => res.json())
    .then(json => {
      console.log(json)
    })
}
document.querySelector('input').addEventListener('change', handlechange, false)
```

``` js
if (url === '/upload') {
  const form = formidable.IncomingForm(), dir = path.resolve(__dirname, "./avatar")
  form.uploadDir = dir

  form.parse(req, (err, fields, files) => {
    console.log(fields, files)
    if (!err) {
      Object.values(files).forEach(({path: oldPath, name}) => {
        fs.rename(oldPath, path.resolve(dir, name), function(err){
          if(err) {
            throw new Error('文件重命名出错...', err)
          }
        })
      })
      res.end(JSON.stringify({success: true}))
    } else {
      throw new Error('文件解析出错...', err)
    }
  })
}
```

**注意：**

#### 1. 请求头问题

使用 fetch / ajax上传文件时，会自动生成一个带有 ` boundary ` 的请求头：

    Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryRj2ZWbdGPDFBuOU8

` boundary ` 用来分割请求体中的每个字段，如果手动设置了请求头`multipart/form-data`，服务端对字段的分割就会报错：

    bad content-type header, no multipart boundary

也就是服务端对文件解析出错。

#### 2. 上传多个文件，加 `multiple` 属性即可；input 文件上传只能兼容 IE10+

#### 3. 上传进度：`XMLHttpRequest` 的 `onprogress` 和 `onloadend` 方法。

#### 4. 文件上传时，解析 multipart/form-data 的请求体可以是 [formidable](https://github.com/felixge/node-formidable)，[multipart](https://github.com/pillarjs/multiparty)也行。
