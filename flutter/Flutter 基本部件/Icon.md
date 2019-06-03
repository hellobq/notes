### 简介 Icon

[Icon](https://api.flutter.dev/flutter/widgets/Icon-class.html) 用于显示 iconfont 的 widget。

使用 icon 的相较于图片的好处有：
- 体积小：可以减小安装包大小。
- 矢量的：iconfont 都是矢量图标，放大不会影响其清晰度。
- 可以应用文本样式：可以像文本一样改变字体图标的颜色、大小对齐等。
- 可以通过 TextSpan 和文本混用。

Icon 的继承关系：

```
Object > Diagnosticable > DiagnosticableTree > Widget > StatelessWidget > Icon
```

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

### 使用Material Design字体图标

Flutter默认包含了一套Material Design的字体图标，在pubspec.yaml文件中的默认配置具有:

``` yaml
flutter:
  uses-material-design: true
```

### 使用自定义图标

在 pubspec.yaml 中声明，icon 名、icon 所在的本地目录、修饰字体（可选）。类似使用自定义字体，在 Flutter 中，使用 .ttf 文件格式即可。

``` yaml
fonts:
  - family: MyIcon
    fonts:
      - asset: fonts/iconfont.ttf
```

为像 materail 自带的 icons 一样方便使用，定义 MyIcons 类：

``` dart
import 'package:flutter/material.dart';

class MyIcons {
  static const password = const IconData(
    0xe680,
    fontFamily: 'MyIcon', 
    matchTextDirection: true
  );
}
```

在其他文件中直接引入 MyIcons、使用 MyIcons 即可：

```
Icon(
  MyIcons.password,
  color: Colors.green
)
```
