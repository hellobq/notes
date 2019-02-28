# cookie

服务器下发浏览器的一小片段数据，当下次请求时，cookie会被携带到服务端。因为HTTP是无状态的，因此常用cookie鉴别用户身份。

- 不能跨域设置、获取cookie。

## 作用

- 会话管理（记录用户登陆状态）
- 跟踪用户行为。用户在首页请求用了cookie，在其他页面请求也用了cookie，那么就可以获取用户访问了什么，记录他的行踪。

## 缺点

- 浏览器每次请求都会携带cookie，即使服务器不需要某个cookie，这样就造成了性能损耗。
- 不安全，不能存储私密信息。CSRF等。
- 存储量小。

## 设置 cookie

可以在response.headers中，通过Set-Cookie字段，设置很多个cookie。

``` js
// node  res.setHeader/res.writeHead都行

res.setHeader('Set-Cookie': ['name=Jack', 'language=javascript'])
```

## cookie 属性

cookie多个属性，对cookie的使用范围做了明确约定。

#### max-age/expires

该cookie的过期时间。max-age代表cookie有效时长，expires代表到何时过期。

``` js
// 2s后，http请求不再携带name这个cookie

res.setHeader('Set-Cookie', ['name=Jack;max-age=2'])

const date = (Date.now() + 2 * 1000).toGMTString()
res.setHeader('Set-Cookie', [`name=Jack;expires=${date}`])
```

#### HttpOnly

浏览器不能通过 **document.cookie** 获取cookie。避免类似CSRF的攻击。

#### secure

比HttpOnly更严格的设置，只能在https请求下，才能带上cookie。同时不能通过 **document.cookie** 获取cookie。

#### domin

可访问cookie的域名（主机名）。默认是当前域名，不同域名（比如：a.test.com和b.test.com）下的cookie是不能共享的，但是可以设置cookie为它们的直接父域名（test.com），那么此时a.test.com就可以使用b.test.com下的cookie了。

``` js
if (req.host === 'test.com') {
  res.writeHead(200, {
    'Set-Cookie': ['name=jack', 'language=javascript;domin=test.com']
  })
}
```

#### path

可访问cookie的路径。即domin + path限制了cookie的作用域。

``` js
// 只能在user目录下，cookie才会被携带到服务器。

res.setHeader('Set-Cookie', ['name=Jack;path=/user'])
```

#### 学习链接

- [MDN cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)
