filename：就是entry文件打包后生成的文件名。

chunkFileName：非entry文件打包后生成的文件名。包括：异步加载的文件、从异步加载/entry文件中split出来的文件名。

有一种情况：就是设置optimization.runtimeChunk（用来管理被分离出来的包）设置为true或者{name: 'runtime'}时，runtime会使用filename命名，而entry文件打包后的文件则使用chunkFileName。
