# stylelint

使用stylelint对样式代码进行检查

## 检查样式步骤

1. 安装包[stylelint stylelint-webpack-plugin](https://github.com/webpack-contrib/stylelint-webpack-plugin)

2. 在webpack配置文件中设置相关选项

``` js
  new StylelintWebpackPlugin({
    configFile: getPath('./.stylelintrc.js'),
    files: ['src/**/*.{s,}css']
  })

```

3. 创建配置文件：[.stylelintrc.js](https://stylelint.io/user-guide/configuration/)

4. 通常会选择stylelint规范，如果觉得规范不合适，可rules字段中实现覆盖。[stylelint-config-recommended/stylelint-config-standrad](https://github.com/stylelint/stylelint-config-recommended)

**注意**

如果使用styled-components，需要特殊配置一下配置（因为style-components有很多功能在规范中是不被允许的）：
https://www.styled-components.com/docs/tooling#stylelint
