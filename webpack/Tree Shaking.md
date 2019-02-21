# Tree Shaking

提出业务中没有用到的代码

## 原理

因为Tree Shaking只支持静态引入，所以对于模块的引入，只能通过ESModule实现。Tree Shaking根据export，只引入导出的内容。

## 怎么做到Tree Shaking

在development下，需要配置optimization.usedExports = true，在package.json文件中设置：sideEffects: ['@babel/ployfill', '\*.scss']告诉Tree Shaking虽然@babel/ployfill、*.scss这类文件没倒出什么东西，仍然要使用，不要把它们屏蔽了。

在production下，optimization.usedExports = true这个配置也不需要的。

## 相关链接

[Tree Shaking](https://webpack.js.org/guides/tree-shaking/#src/components/Sidebar/Sidebar.jsx)
