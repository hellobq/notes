# entry

webpack的入口文件

## 什么是entry?

webpack开始构建的入口点，默认值是'./src/index.js'。当然，可以手动设置一个/多个入口点。

## 语法规则：

单入口点（单页应用）可以使用字符串/对象形式。

``` js
module.exports = {
  entry: './path/to/my/entry/file.js'
}

module.exports = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
}

```

## 多入口点（多页应用）只能对象形式

``` js
module.exports = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
}

```

## entry是数组

它表示一个打包入口，打包的入口文件需要依赖前者的注入。

module.exports = {
  entry: {
    pageOne: ['babel-polyfill', 'react-hot-loader/patch', './src/pagrOne.js']
  }
}
