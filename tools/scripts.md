# npm script

## 快速创建package.json文件？

(npm/yarn) init [-y] 

## 为什么执行npm test，就会执行scripts内部的命令呢？

因为npm在运行scripts之前，会把node_modules/.bin加到环境变量$path之前。

## npm scripts 多个命令如何串行和并行？

- 串: 命令1 && 命令2  并: 命令1 & 命令2
- npm-run-all

## 如何设置环境变量？

cross-env

## scripts的平台兼容问题？
- 项目中使用的第三方库已经提供了兼容命令。
- 所有需要使用引号的地儿，都换成双引号，且转义。

