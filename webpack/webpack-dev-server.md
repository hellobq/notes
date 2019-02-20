# webpack-dev-server

前端开发的小型服务器，能帮助快速开发应用程序。webpack能够对源文件进行实时地监听打包，每次打包都需要手动移除原来的dist文件夹（当然，可以用clean-webpack-plugin插件），生成新的dist文件后手动再打开到浏览器上预览。代码稍微改一下，就得重复上面动作，这..开发效率就打折扣了。于是webpack-dev-server就出现了。

## 作用

- 实时监听源代码，并重新打包（webpack也能通过--watch做到）。
- 把打包后的文件放到了内存中，因此并不能看见打包后的dist文件夹。
- 内部是一个node起的服务器，代码修改时，服务器可以感知到。通过配置devServer配置后，可实现热替换。
- 更改host地址，方便调试，设置端口，避免冲突。
- 代理服务，实现dev环境下的跨域。
- .....

## opts:

[public](https://webpack.js.org/configuration/dev-server/#devserver-public) 用于指定静态服务的域名，默认是 http://localhost:8080/ ，当你使用 Nginx 来做反向代理时，应该就需要使用该配置来指定 Nginx 配置使用的服务域名。

[publicPath](https://webpack.js.org/configuration/dev-server/#devserver-proxy)：设置内存中打包后的文件输出目录，把bundle.js放到指定目录下。默认下打包后访问地址是http://localhost:8080/index.html（也就是devServer.publicPath === output.publicPath的，这样就保证打包前后访问地址相同啦），设置此参数后就变成http://localhost:8080/project/index.html

``` js
publicPath: '/project/'

```

[proxy](https://github.com/chimurai/http-proxy-middleware)：dev环境下的代理跨域。devServer借助http-proxy-middkeware中间件实现的。

``` js
module.exports = {
  //...
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        changeOrigin: true,
        pathRewrite: {
            '^/api' : ''
        }
      }
    }
  }
}

```

[host](https://webpack.js.org/configuration/dev-server/#devserver-host)：设定服务器的域名。默认是localhost，为方便调试，可以将其修改成 '0.0.0.0' 。

``` js
host: '0.0.0.0' 或 --host 0.0.0.0

```

[port](https://webpack.js.org/configuration/dev-server/#devserver-port)：设定服务器端口。

``` js
port: 8080 或 --port 8080

```

[contentBase](https://webpack.js.org/configuration/dev-server/#devserver-contentbase)：告诉服务器从哪里提供内容。使用绝对路径；要禁用：contentBase: false即可。如果使用了 [copy-webpack-plugin](https://webpack.js.org/plugins/copy-webpack-plugin/#src/components/Sidebar/Sidebar.jsx) 就不用这个了。

``` js
contentBase: path.join(__dirname, './dist')  或   --content-base dist(./dist一样的)

```

[compress](https://webpack.js.org/configuration/dev-server/#devserver-compress)：为指定目录下的文件开启[gizp](https://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression/)压缩。

``` js
compress: true 或 --compress

```

[historyApiFallback](https://webpack.js.org/configuration/dev-server/#devserver-historyapifallback)：当使用h5的history API时，如果在地址栏输入不存在的路由时，它会跳转到首页。

``` js
historyApiFallback: true 或 --history-api-fallback

```

[progress](https://webpack.js.org/configuration/dev-server/#devserver-progress-cli-only)：打印打包的进度。只能在cli内设置。

```js
--process

```

[clientLogLevel](https://webpack.js.org/configuration/dev-server/#devserver-clientloglevel)：控制台log的输出。如果设置'none'，在浏览器console中将不会出现大串的打包进度打印。

``` js
clientLogLevel: 'none' 或  --client-log-level none

```

[open](https://webpack.js.org/configuration/dev-server/#devserver-open)：dev-server服务启动后打开服务器。默认是禁用。

``` js
open: true 或 --open

```

[hot](https://webpack.js.org/configuration/dev-server/#devserver-hot)：开启[热替换](https://webpack.js.org/concepts/hot-module-replacement/)功能。还得手动添加[HotModuleReplacementPlugin](https://webpack.js.org/plugins/hot-module-replacement-plugin/#src/components/Sidebar/Sidebar.jsx)插件，然后在需要热更新的文件书写一段js代码。但是，能局部更新，但是记录不了之前更新的状态，遂使用[react-hot-loader](https://github.com/gaearon/react-hot-loader)。（不过当代码中使用类修饰器时，再使用react-hot-loader组件就不能实现热更新，截至2018-12-21还未修复）。所以这个轮子可暂时不用，状态的恢复再手动一下吧....

``` js
hot: true 或 --hot

plugins: [new webpack.HotModuleReplacementPlugin()]

// 我要热更新App这个根组件
module.hot && module.hot.accept(App)

/* 
  引入react-hot-loader后，修改入口entry，
  给.babelrc.js的plugins添加一个配置项："react-hot-loader/babel"
*/
entry: {
  app:  ['react-hot-loader/patch', './src/index.js']
}
"plugins": [
  "@babel/plugin-transform-runtime",
    
  // 允许class组件内写公共属性（在配置react一文中也有介绍）
  "@babel/plugin-proposal-class-properties", 
  "react-hot-loader/babel"
]

```

[overlay](https://webpack.js.org/configuration/dev-server/#devserver-overlay)：（default false）当编译器遇到警告和错误时，会覆盖浏览器全屏。

``` js
overlay: true 
或
overlay: {
  warnings: true,
  error: true
}

```

