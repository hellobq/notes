# url

[url](http://nodejs.cn/api/url.html#url_url) 是 node 中的内置模块，用来处理和解析 url。

## url模块中的属性和方法

url.hash 获取url中的hash部分。

url.protocol: 获取协议

url.host 获取主机部分（不包含协议）。

url.hostname: 也是获取主机部分（不包含协议、端口）。

url.port: 获取端口

url.origin: 获取origin部分（不包括路径）。

url.pathname: 获取url中的路径部分。

url.href: 获取整个请求url。

url.query: 获取queryString（?以后的部分）

**注意**

在使用上述方法之前，要先创建Url实例，然后才能调用相关属性：

``` js
const { URL } = require('url')

const url = new URL('https://www.baidu.com')

console.log(
  url.protocol,
  url.origin,
  url.port,
  url.pathname,
  url.href,
  url.query,
  url.hash
)

// https: https://www.baidu.com  / https://www.baidu.com/ undefined
```

## 不创建 url 示例，直接解析

``` js
const url = require('url')
const website = 'https://www.baidu.com'

// 第二个参数设置为 true，将 query 转换成对象。
url.parse(website, true)

/*
  Url {
    protocol: 'https:',
    slashes: true,
    auth: null,
    host: 'www.baidu.com',
    port: null,
    hostname: 'www.baidu.com',
    hash: null,
    search: null,
    query: {},
    pathname: '/',
    path: '/',
    href: 'https://www.baidu.com/' 
  }
*/
```
