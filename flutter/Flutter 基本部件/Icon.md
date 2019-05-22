### 简介 Icon

[Icon](https://api.flutter.dev/flutter/widgets/Icon-class.html) 用于显示 iconfont 的 widget。

使用 icon 的相较于图片的好处有：
- 体积小：可以减小安装包大小。
- 矢量的：iconfont 都是矢量图标，放大不会影响其清晰度。
- 可以应用文本样式：可以像文本一样改变字体图标的颜色、大小对齐等。
- 可以通过 TextSpan 和文本混用。

Icon 的继承关系：

    Object > Diagnosticable > DiagnosticableTree > Widget > StatelessWidget > Icon

### Icon 的构造函数及参数说明

``` dart
class Icon extends StatelessWidget {

  const Icon(@required this.icon, {
    Key key,
    this.size,
    this.color,
    this.semanticLabel,
    this.textDirection,
  }) : super(key: key);
  
  ...
}
```

参数名字	| 参数类型	| 意义	| 必选 or 可选
- | - | - | - 
key	  | Key	    | Widget 的标识	| 可选
color	| double	| icon的大小（主要）| 可选
size	| Color	  | icon的颜色（主要）| 可选
semanticsLabel	| String        | 给 Image 加上一个语义标签，没有实际用处	  | 可选
textDirection	| TextDirection	| Icon的绘制方向	| 可选
