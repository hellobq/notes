# optimization.splitChunks

分解main.bundle.js为多个小的js文件，这样做的好处：
- 用户加载js业务逻辑不再需要等在main.bundle.js加载完成后，再显示了。
- 为了缓存着想。打包后不同的js chunk对应的hash不同，某个js代码改变，用户只要重新缓存这一个小小的chunk就行，其他小的chunk缓存可以继续使用的。

## 参数详解

chunks: 对异步代码('async')、同步代码('initial')、同步且异步的代码('all')做分割。对于同步加载的代码，还会根据cacheGroups区分，进入哪个组。

minSize: 如果想要分离的js chunk大小小于minSize，那么它不会打包成一个js chunk。一般设置为30000（30kb）。

maxSize: 告诉webpack如果js chunk大于maxSize，将会被分割成更小的chunks，且每个chunks大小要大于minSize。（可不配）

minchunks: 共享该模块的最小chunks数。（默认是1，可不配）

maxAsyncRequests: 按需加载时，最大的并行请求数。

maxInitialRequests: 一个入口点最大的并行请求数，如果大于这个数，将不再做代码分割。

automaticNameDelimiter: chunk文件名的分隔符。

name: 拆分块的名称，设置成true表示基于块和缓存组的key组成的名字，用automaticNameDelimiter分割。

cacheGroups: 把拆分块分到哪个文件中。

cacheGroups.key.test：控制该缓存组匹配的模块。

cacheGroups.key.filename: 拆分块的名字。

cacheGroups.key.priority: 设置每个缓存组的优先级，同优先级下按照拆分块的文件大小。

cacheGroups.key.reuseExistingChink: 一个模块已经打包过，就不再打包了，重用上次打包的结果就行。

cacheGroups.key.enforce：告诉webpack忽略splitChunks.minSize，splitChunks.minChunks，splitChunks.maxAsyncRequests和splitChunks.maxInitialRequests选项，并始终为此缓存组创建块。

## optimization.splitChunks 的默认配置

``` js
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'async',
      minSize: 30000,
      maxSize: 0,
      minChunks: 1,
      maxAsyncRequests: 5,
      maxInitialRequests: 3,
      automaticNameDelimiter: '~',
      name: true,
      cacheGroups: {
        vendors: {
          test: /[\\/]node_modules[\\/]/,
          priority: -10
        },
        default: {
          minChunks: 2,
          priority: -20,
          reuseExistingChunk: true
        }
      }
    }
  }
}

```
