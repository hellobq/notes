# mode

告诉webpack所处的打包模式，是开发模式development还是生产模式production。针对两种模式，会做不同的配置。
 
- 生产环境可能需要分离 CSS 成单独的文件，以便多个页面共享同一个 CSS 文件
- 生产环境需要压缩 HTML/CSS/JS 代码
- 生产环境需要压缩图片
...

- 开发环境需要生成 sourcemap 文件
- 开发环境需要打印 debug 信息
- 开发环境需要 live reload 或者 hot reload 的功能
...

## webpack 默认的mode配置

默认是 'production'，它会自动对代码压缩。

## 设置mode

在json配置文件中配置mode属性，在scripts配置。

``` js
module.exports = {
  mode: 'development'
};

webpack --mode=production

```

## 相关链接

https://medium.com/webpack/webpack-4-mode-and-optimization-5423a6bc597a
