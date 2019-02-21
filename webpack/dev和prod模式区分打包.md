# dev和prod分开打包

在两种模式下的打包机制是不同的具体如下：
- dev需要完整的sourceMap, HMR, webpack-dev-server,等。
- prod要做打包优化：代码压缩、代码分割、做hash, 去掉sourceMap, HMR, webpack-dev-server等。
- 使用webpack-merge合并dev、prod公有的配置。

