# 打包js

转es6+为es5, 兼容低版本浏览器。

## 安装的模块

babel-loader: babel和webpack的桥梁，但是还是需要其他模块来转换最新的es6+语法。

@babel/preset-env: 语法转换

@babel/plugin-transform-runtime: 转换@babel/preset-env未转变的代码

## 在modle.rule中的配置

``` js
rule: [{
  test: /\.js$/,
  loader: 'babel-loader',
  exclude: /node_modules/
}]

```

## 把babel相关配置放到.babelrc.js这个单独的文件中

``` js
module.exports = {
  presets: ['@babel/preset-env'],
  plugins: [
    "@babel/plugin-transform-runtime"
  ]
}

```

## 打包react

react、react-dom

@babel/preset-react: 打包react语法

@babel/plugin-syntax-dynamic-import: 支持异步加载

@babel/plugin-proposal-class-properties: 使得react class组件内能声明局部变量

@babel/plugin-proposal-decorators: 能使用类修饰器

``` js
module.exports = {
  "presets": [
    "@babel/preset-react",
    [
      "@babel/preset-env",
      {
        "targets": "> 0.25%, not dead"
      }
    ]
  ],
  "plugins": [
    "@babel/plugin-transform-runtime",
    [
      "@babel/plugin-proposal-decorators", { 
        "legacy": true
      }
    ],
    [
      "@babel/plugin-proposal-class-properties", {
        "loose": true
      }
    ],
    "@babel/plugin-syntax-dynamic-import"
  ]
}

```


