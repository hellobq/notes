# yarn

## 安装 yarn

下载并安装 [yarn](https://yarnpkg.com/lang/zh-hans/docs/install/#windows-stable)

## yarn 常用命令

- yarn(install) 安装所需依赖
- yarn init -y 初始化项目，采用默认信息
- yarn add package-name [-D] 安装依赖到生产环境/开发环境
- yarn global add package-name 安装依赖到全局环境
- yarn upgrade package-name [-D] 在生产环境/开发环境中升级依赖
- yarn (run) scripts-name 运行scripts
- yarn remove package-name [-D] 在生产环境/开发环境中卸载模块
- yarn info package-name 查看包的相关信息（包括versions、size等）

## Yarn 和 npm 命令对比

- npm i === yarn
- npm i package-name -S === yarn add package-name
- npm uninstall package-name -S === yarn remove package-name
- npm i package-name -D === yarn add package-name -D
- npm i package-name -g === yarn global add package-name
- npm update package-name [-S] === yarn upgrade package-name [-D]

## 查看源和换源

- npm/yarn config get registry                                            
- npm/yarn config set registry https://registry.npm.taobao.org/  
## 镜像源地址部分如下：使用nrm来管理源）

- npm --- https://registry.npmjs.org/
- cnpm --- https://r.cnpmjs.org/
- taobao --- https://registry.npm.taobao.org/
- nj --- https://registry.nodejitsu.com/
- rednpm --- https://registry.mirror.cqupt.edu.cn/
- npmMirror --- https://skimdb.npmjs.com/registry/
- deunpm --- http://registry.enpmjs.org/

## 查看npm/yarn全局安装的包

- npm list -g --depth 0
- yarn global list

