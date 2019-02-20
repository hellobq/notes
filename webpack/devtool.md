# devtool

对源js文件产生映射，如果打包后的js代码在浏览器上出错，那么会立即定位到源代码出错之处。

## development：cheap-module-eval-source-map

inline: 把打包生成的.map文件放到目标文件的最后。

cheap: 只提示多少行，不提示列出错。只负责业务逻辑的出错。

module：第三方依赖的出错，比如loader中的出错。

eval: 一起执行业务代码和sourceMap。能提高打包速度。但是不太安全。

能打印出较全的错误信息，包括逻辑代码、第三方模块的信息，挺快。

## production: cheap-module-source-map

