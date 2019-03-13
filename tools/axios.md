# axios：更高效的 http 请求库

相对于 `fetch`，有：

- 可用在客户端和服务端
- 超时控制
- 兼容性更强
- 请求和响应的拦截
- 监控文件上传的进度
- ...

## get 请求

#### axios.get(url[, config]) 或者 axios(config)

``` js
axios.get('http://localhost:9000/demo', {  /* url 也可以拼接 */
  params: {
    name: 'Bob',
    age: 20
  }
})
  .then(res => {
    console.log(res)
  })
  .catch(err => {
    console.log(err)
  })


const getData = async () => {
  try {
    const { data } = await axios.get('http://localhost:9000/demo', {
      params: { 
        name: 'Bob', 
        age: 20 
      }
    })

    console.log(data)
  } catch(err) {
    console.log(err)
  }
}
```

## post 请求

#### axios.post(url[, data][, config]) 或者 axios(config)

``` js
async getData () {
  let name = 'Bob', age = 20
  try {
    const { data } = await axios.post(`http://localhost:9000/teacher`, {
      name,
      age
    })

    console.log(data)
  } catch(err) {
    console.log(err)
  }
}
```

## axios 并发控制

#### axios.all([req1. req2])

``` js
axios.all([
  axios.post('http://localhost:9000/teacher'),
  axios.post('http://localhost:9000/student')
])
  .then(([{data: data1}, {data: data2}]) => {
    console.log(data1, data2)
  })
  .catch(err => {
    console.log(err)
  })
```

## axios 配置 demo

#### axios(config)

``` js
axios({
  method: 'post',
  url: 'http://localhost:9000/teacher',
  body: {
    name: 'Bob',
    age: 20
  },
  withCredentials: true  /* 后台需要设置 origin/credentials */
})
  .then(({data}) => {
    console.log(data)
  })
  .catch(err => { console.log(err) })
```

## 请求方法的别名

对于每个请求方式，都有一个别名。

``` js
axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.options(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
```

## 并发请求

```js
axios.all(iterable)
axios.spread(callback)
```

## 创建 axios 实例

使用自定义配置，来创建 axios 实例。

``` js
axios.create([config])

const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
})
```

## 实例方法

每个 axios 指定的配置会和实例配置合并。

``` js
axios#get(url[, config])
axios#delete(url[, config])
axios#head(url[, config])
axios#options(url[, config])
axios#post(url[, data[, config]])
axios#put(url[, data[, config]])
axios#patch(url[, data[, config]])
axios#getUri([config])
```

## axios 具体配置

``` js
{
  // 请求地址
  url: '/user',

  // 请求方法，默认是 get
  method: 'get', // default

  // 如果 url 是相对的，baseURL 会 拼接它
  baseURL: 'https://some-domain.com/api/',

  // 数据协商使得，在数据发送之前，可以整理多次。
  // 仅适用于 PUT、POST、PATCH
  // 最后一个函数必须返回字符串或者Buffer/ArrayBuffer/FormData/Stream的实例
  transformRequest: [function (data, headers) {
    return data;
  }],

  // 在相应之前更改数据，然后传给then/catch
  transformResponse: [function (data) {
    return data;
  }],

  // 自定义头部信息
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // get 请求是发送的数据
  params: {
    ID: 12345
  },

  // 在其中使用 qs 来序列化 params
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function (params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // 请求体发送的数据
  // 仅支持的请求方式：'PUT', 'POST', and 'PATCH'
  // 当 `transformRequest` 没设置时, 必须是以下类型之一: string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // 在浏览器中： FormData, File, Blob
  // 在 Node 中： Stream, Buffer
  data: {
    firstName: 'Fred'
  },

  // 毫秒数 请求时间超过 timeout，将会被终止
  timeout: 1000, // default is `0` (no timeout)

  // 是否可发送 cookies
  withCredentials: false, // default

  // `adapter` allows custom handling of requests which makes testing easier.
  // Return a promise and supply a valid response (see lib/adapters/README.md).
  adapter: function (config) {
    /* ... */
  },

  // `auth` indicates that HTTP Basic auth should be used, and supplies credentials.
  // This will set an `Authorization` header, overwriting any existing
  // `Authorization` custom headers you have set using `headers`.
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // 服务器将响应的数据类型：'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default

  // 解码响应的内容
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // default

  // `xsrfCookieName` is the name of the cookie to use as a value for xsrf token
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default

  // 上传进度事件
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // 下载进度事件
  onDownloadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // 以字节为单位，定义响应内容的最大大小
  maxContentLength: 2000,

  // `validateStatus` defines whether to resolve or reject the promise for a given
  // HTTP response status code. If `validateStatus` returns `true` (or is set to `null`
  // or `undefined`), the promise will be resolved; otherwise, the promise will be
  // rejected.
  validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },

  // `maxRedirects` defines the maximum number of redirects to follow in node.js.
  // If set to 0, no redirects will be followed.
  maxRedirects: 5, // default

  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default

  // `httpAgent` and `httpsAgent` define a custom agent to be used when performing http
  // and https requests, respectively, in node.js. This allows options to be added like
  // `keepAlive` that are not enabled by default.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' defines the hostname and port of the proxy server.
  // You can also define your proxy using the conventional `http_proxy` and
  // `https_proxy` environment variables. If you are using environment variables
  // for your proxy configuration, you can also define a `no_proxy` environment
  // variable as a comma-separated list of domains that should not be proxied.
  // Use `false` to disable proxies, ignoring environment variables.
  // `auth` indicates that HTTP Basic auth should be used to connect to the proxy, and
  // supplies credentials.
  // This will set an `Proxy-Authorization` header, overwriting any existing
  // `Proxy-Authorization` custom headers you have set using `headers`.
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` specifies a cancel token that can be used to cancel the request
  // (see Cancellation section below for details)
  cancelToken: new CancelToken(function (cancel) {
  })
}

```

## axios 小封装

``` js
//引入axios
import axios from 'axios'

let cancel ,promiseArr = {}
const CancelToken = axios.CancelToken;

//请求拦截器
axios.interceptors.request.use(config => {
    //发起请求时，取消掉当前正在进行的相同请求
    if (promiseArr[config.url]) {
        promiseArr[config.url]('操作取消')
        promiseArr[config.url] = cancel
    } else {
        promiseArr[config.url] = cancel
    }
      return config
}, error => {
    return Promise.reject(error)
})

//响应拦截器即异常处理
axios.interceptors.response.use(response => {
    return response
}, err => {
    if (err && err.response) {
      switch (err.response.status) {
        case 400:
          err.message = '错误请求'
          break;
        case 401:
          err.message = '未授权，请重新登录'
          break;
        case 403:
          err.message = '拒绝访问'
          break;
        case 404:
          err.message = '请求错误,未找到该资源'
          break;
        case 405:
          err.message = '请求方法未允许'
          break;
        case 408:
          err.message = '请求超时'
          break;
        case 500:
          err.message = '服务器端出错'
          break;
        case 501:
          err.message = '网络未实现'
          break;
        case 502:
          err.message = '网络错误'
          break;
        case 503:
          err.message = '服务不可用'
          break;
        case 504:
          err.message = '网络超时'
          break;
        case 505:
          err.message = 'http版本不支持该请求'
          break;
        default:
          err.message = `连接错误${err.response.status}`
      }
    } else {
      err.message = "连接到服务器失败"
    }
    message.err(err.message)
      return Promise.resolve(err.response)
})

axios.defaults.baseURL = '/api'
axios.defaults.headers = {
    'X-Requested-With': 'XMLHttpRequest'
}
axios.defaults.timeout = 10000

export default {
  //get请求
    get (url,params) {
      return new Promise((resolve,reject) => {
        axios({
          method: 'get',
          url,
          params,
          cancelToken: new CancelToken(c => {
            cancel = c
          })
        }).then(res => {
          resolve(res)
        })
      })
    },
  //post请求
    post (url,param) {
      return new Promise((resolve,reject) => {
        axios({
          method: 'post',
          url,
          data: param,
          cancelToken: new CancelToken(c => {
            cancel = c
          })
        }).then(res => {
          resolve(res)
        })
      })
     }
  }

```
