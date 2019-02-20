# plugin

使用loader能够实现转换某些类型的模块，但是通过添加plugin，完成构建的特殊需求。比如：静态资源优化，注入全局变量等。

## html-webpack-plugin 

[html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin#options) 打包结束后自动生成个html文件，把css、js文件自动引入html中。

``` js
yarn add html-webpack-plugin -D

const HtmlWebpackPlugin = require('html-webpack-plugin')

plugins: [
  new HtmlWebpackPlugin({
    template: './src/index.html'
  })
]

```

## copy-webpack-plugin

[copy-webpack-plugin](https://github.com/webpack-contrib/copy-webpack-plugin) 把未经webpack处理的文件也放在build目录下。

``` js
yarn add copy-webpack-plugin -D

const CopyWebpackPlugin = require('copy-webpack-plugin')

plugins: [
  new CopyWebpackPlugin([
    { from: 'src/file.txt', to: 'build/file.txt', }, // 顾名思义，from 配置来源，to 配置目标路径
    { from: 'src/*.ico', to: 'build/*.ico' }, // 配置项可以使用 glob
    // 可以配置很多项复制规则
  ]),
],

```

## clean-webpack-plugin

在打包之前执行这个plugin，自动删除上次打包的目录

``` js
yarn add clean-webpack-plugin -D

const CleanWebpackPlugin = require('clean-webpack-plugin')

plugins: [
  new CleanWebpackPlugin(['dist'])
]

```

## ProvidePlugin

[ProvidePlugin](https://webpack.docschina.org/plugins/provide-plugin/)webpack内置插件，避免在A.js、B.js引入C.js这种情况。

## 相关链接

[webpack plugins汇总](https://github.com/webpack-contrib/awesome-webpack#webpack-plugins)

