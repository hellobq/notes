# loader

webpack不能自动打包非js类型的资源文件，需要loader用来辅助webpack打包。

## 怎么配置loader?

自然在module.rules属性内配置，配置是需要注意：

- 不同类型的文件，可能会使用不同的loaders。
- 对于同一种文件，可能使用多种loaders，loaders的书写顺序和作用顺序相反。
- 对于不同的loaders，会有不同的opts。

``` js
// 打包 .css样式文件

module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          }
        ]
      }
    ]
  }
}

```


