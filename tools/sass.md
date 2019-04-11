# sass

文件后缀名是：.scss

每行样式后，要加分号。否则后面的样式无效。

注释：
- 单行注释：//
- 多行注释：/**/，会保留在编译后的css文件内。

为避免重复写样式，使用样式地嵌套，其中&代表父级选择器。

scss文件地嵌套：
- 可以在一个.scss文件任意处，使用@import引用其他scss文件；
- 引用多个文件：@import 路径1, 路径2；

定义变量：
- $arg-name: arg-value，尽量使用破折号代替下划线。
- 可在不同作用域（层级样式）内定义变量，变量可在作用域范围内相互引用。

定义函数：使用@function定义函数，@return返回值。例如：

```scss
/* 在小程序内iphone6下， px2rpx */

@function px2rpx($px: 10) {
  @return $px * 2rpx
}

.box {
  width: px2rpx();
}
```

定义mixin：@mixin定义，@include引入 (也可以使用动态参数)。

```scss
@mixin mixin() {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.box {
  @include mixin;
}
```

@if/@else 实现 toogle:

``` scss
@mixin toogle ($flag: true) {
  @if $flag {
    display: block;
  } @else {
    display: none;
  }
}

.box {
  @include toogle()
}
```

@for 循环:

``` scss
@for $i from 1 through 10 {
  .box-#{$i} {
    display: inline-block;
  }
}
```

@while 循环：

``` scss
$i: 0;
@while $i <= 10 {
  .box-#{$i} {
    display: inline-block;
  }
  $i: $i + 1;
}
```

@each 枚举遍历：

``` scss
$num: 1 2 3 4;

@each $i in $num {
  .box-#{$i} {
    display: inline-block;
  }
}
```

打包scss文件：

```js
/* webpack: 安装style-loader、node-sass、sass-loader、css-loader */

{
    test:/\.scss$/,
    use: {
        fallback: 'style-loader',
        use:['css-loader', 'sass-loader']
    },
    exclude: /node_modules/
}


/* gulp: 安装gulp-sass插件 */

```

相关链接：
- [sass参考手册](http://sass.bootcss.com/docs/sass-reference/)
