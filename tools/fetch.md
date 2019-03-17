# fetch: 基于 `promise` 的 `ajax`

`fetch` 是高级浏览器 `window` 对象下挂载的一个 function，用来做异步请求的。

``` js
fetch(url, opts).then(function(response) {
  // 处理 HTTP 响应
}, function(error) {
  // 处理网络错误
})
```

fetch 有两个参数：

&nbsp;&nbsp; input：url 或者 [Request](https://developer.mozilla.org/zh-CN/docs/Web/API/Request) 对象

&nbsp;&nbsp; opts: 请求的配置参数

> method: 请求使用的方法，如 GET、POST。</br>
  headers: 请求的头信息，包含与请求关联的Headers对象。</br>
  body: 请求的 body 信息。注意 GET 或 HEAD 方法的请求不能包含 body 信息</br>
  mode: 请求的模式，如 cors（默认）、 no-cors 或者 same-origin。</br>
  credentials: 请求的 credentials，如 omit（不发送cookies）、same-origin（同源发送cookies） 或者 include（跨域发送cookies）。

## 常用的 fetch 请求

``` js
/*
  请求文本文件
*/

fetch('/index/fetchHtml')
  .then(res => res.text())
  .then(text => {
    console.log(text)
  })
  .catch((err) => {
  })

/*
  请求json文件
*/

fetch('/index/fetchJson')
  .then(res => res.json())
  .then(json => {
    console.log(json)
  })
  .catch((err) => {
  })

/*
  请求img blob文件
*/

fetch('/index/fetchImg')
  .then(res => res.blob())
  .then(imgBlob => {
    const img = new Image()
    img.src = URL.createObjectUrl(imgBlob)
    img.onload = function() {
      URL.revokeObjectURL(this.src);
    }
    document.body.appendChild(img)
  })
  .catch((err) => {})

/*
  form 表单
*/
function postForm() {
  const form = document.querySelector('form')
  const name = encodeURI(document.getElementsByName('name')[0].value)
  
  fetch(`/api/user/${name}`, {
    method: 'POST',

    // 使用这种格式，需要序列化 form data
    headers: {
      "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"
    },
    body: new FormData(form)
  })
}

fetch('http://localhost:4321/api/registry', {
  method: 'POST',

  // 使用这种内容格式，不需要序列化  request payload
  headers: {
    "Content-type": "application/json"
  },
  body: JSON.stringify({
    1: 2,
    3: 4
  })
}) 
  .then(data => data.json())
  .then(json => {
    console.log(json)
  }) 
  .catch(err => {})
```

## fetch 注意事项

只要网络错误情况下，才会走 `reject`，否则一直 `resolve`（即使 404）。所以需要在 `response` 处判断 ok 或者 status 字段。

``` js
fetch('http://localhost:9000/demo.json')
  .then(res => {
    if (!res.ok) {
      console.log(`Looks like there was a problem. Status Code: ${ response.status }`);
      return;
    }

    return res.json()
  })
  .then(json => {
    console.log(json)
  })

```

## 跨域 cookie 的传输

1. fetch 请求时设置 `credentials: 'include'`，表示即使不同源，也会伴随 `ajax` 发送到后台。
2. 对于跨域请求，后台需要设置：`Access-Control-Allow-origin: 'http://localhost:8000'`（不可设置为 *）  `Access-Control-Allow-Credentials: true`

## 超时控制

一段时间后未返回结果，就不用请求的结果啦（其实请求还在继续）。

``` js
const abort = () => {
  Promise.race([
    fetch('http://localhost:1000/demo.json'),
    
    new Promise((resolve, reject) => {
      setTimeout(() => reject(new Error('request timeout')), 1000)
    })
  ])
    .then(res => {
      console.log(res)
    })
    .catch(err => {
      console.log(err)
    })
}
```

## fetch 比原生 ajax 的优点

- 基于 `Promise`，比 `XMLHttpRequest` 使用简洁。XHR 设计复杂，写的代码更多。
- 可自定义是否携带 cookie。

## fetch 的 `polyfill` 

[fetch](https://github.com/github/fetch) 只能兼容到 ie10+

低版本浏览器还得用 `jsonp` 或 原生 `ajax`。fetch 不支持 jsonp。

[node-fetch](https://github.com/bitinn/node-fetch): 在 node 中使用 fetch。
