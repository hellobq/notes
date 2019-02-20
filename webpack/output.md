# output

webpack构建后的[output](https://webpack.js.org/concepts/output/)（静态资源打包后所处的目录），也可以指定单出口/多出口。默认输出文件是 './dist/main.js'

## 语法规则：

需要配置出口文件名filename和路径path。

``` js
const { resolve } = require('path')

// 单出口
module.exports = {
  output: {
    filename: 'bundle.js',
    path: resolve(__dirname, './dist')
  }
}

// 多出口
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',               // 这个name就是entry对象的key
    path: resolve(__dirname, './dist')
  }
}

```

## 高级用法

当打包成静态资源时，会扔到cdn上。

为了避免资源缓存对cdn更新的影响，会给每个打包出来的文件加一段hash值（如果源文件代码变化，会打包成新的hash值）。

使用publicPath属性：设置静态资源的公共路径。

``` js
// 多出口
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].[hash:8].js',
    path: resolve(__dirname, './dist'),
    publicPath: 'http://cdn.example.com/assets/[hash:8]/'
  }
};

```
