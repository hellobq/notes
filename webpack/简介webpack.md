# 简介 webpack

一个模块打包工具，按照模块引入方式，把项目源代码（一个个的模块）打包到一起，让浏览器（宿主环境）能识别和运行打包后的代码。

## webpack 打包的模块引入方式

- ESMoudle import引入 (webpack 推荐)
- CommonJS require引入
- AMD define/require引入
- 样式文件 @import方式引入
- 图片文件引入 url、src

## esmodule、commonjs、AMD模块引入的区别

import是esmodule静态引入模块的方式，因为import不能在业务逻辑中引入模块。通过export导出模块。

commonjs通过require引入、module.exports导出，支持动态模块的导入，即可在业务逻辑中引入模块。

AMD通过define定义模块、require引入模块。并且模块的定义是后者依赖前者。

## 全局安装和局部安装

推荐局部安装webpack。因为全局安装的webpack版本只是一个，并且是固定的。如果对于两个项目所依赖的webpack版本不一致（一个3.x，一个4.x），那么全局安装的webpack就不合适了。

## 在安装webpack时，为什么需要安装webpack-cli?

使得webpack能够在命令行内运行。

## webpack打包后信息中：chunks和chunknames啥意思？

webpack打包js文件后，js文件的id和文件名


