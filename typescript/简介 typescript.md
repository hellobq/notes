### 简介 typescript

- 微软开发的开源语言。
- 它是JS的超集，遵循ECMAScript规范，拓展了javascript的语法。
- 具有静态类型检查、能开发大型项目等优势。

### 对比 javascript

关系：遵循JS语法，可顺利进阶TS，TS也可以编译为JS。

- 同：开源、跨平台。
- 异：
  + 定义为开发大型应用的语言，比JS作用范围更广。
  + TS提供了类、接口、模块，更利于组件的开发和维护。

### 安装 typescript

使用 npm/yarn 全局安装 typescript 即可。

``` bash
npm i typescript -g

或

yarn global add typescript
```

### 初步使用 ts

1. 创建 demo.ts 文件。
2. 使用 `tsc demo.ts` 编译当前 ts 文件，编译成 js 文件。

### 通过编辑器（vscode）来自动编译 ts 文件

每次更改 ts 文件，再手动执行 `tsc 文件名` 太麻烦了，自动编译 ts 文件更好：

1. 使用命令 `tsc --init` 生成 ts 配置文件 `tsconfig.json`。
2. 点击菜单 > 任务 > 运行工具，点击 `tsc：监视 - tsconfig.json` 文件即可（注意终端不能是 git bash，否则找不到 tsconfig.json 文件）。

另外：在 rollup、webpack 打包工具中，也能自动编译 ts 文件。
