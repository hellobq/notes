### 1. 简介 Text

用来展示文本的小部件，[Text](https://api.flutter.dev/flutter/widgets/Text-class.html) 的用法如下：

``` dart
(new) Text(
  String data, 
  Key key, 
  TextStyle style, 
  StrutStyle strutStyle, 
  TextAlign textAlign, 
  TextDirection textDirection, 
  Locale locale, 
  bool softWrap, 
  TextOverflow overflow, 
  double textScaleFactor, 
  int maxLines, 
  String semanticsLabel
}) → Text
```

参数名字 | 参数类型 | 意义 | 必选 or 可选
- | - | - | -
data | String |	要显示的文字 | 必选
key	| Key	| Widget 的标识	| 可选
style	| TextStyle	| 文本样式	| 可选
strutStyle	| StrutStyle	| 设置每行的最小行高	| 可选
textAlign	| TextAlign	| 文本的对齐方式	| 可选
textDirection	| TextDirection	| 文字方向	| 可选
locale	| Locale	| 用于选择用户语言和格式设置首选项的标识符	| 可选
softWrap	| bool	| 是否支持软换行符<br>如果是 false 的话，这个文本只有一行，水平方向是无限的	| 可选
overflow	| TextOverflow	| 文本的截断方式	| 可选
textScaleFactor	| double	| 代表文本相对于当前字体大小的缩放因子<br>默认值为1.0	| 可选
maxLines	| int	| 显示的最大行数	| 可选
semanticsLabel	| String	| 给文本加上一个语义标签<br>没有实际用处	| 可选

#### textAlign：文本的对齐方式

当 Text 宽度大于文本内容长度时，textAlign 用来设置字体对齐方式。

TextAlign 值 | 含义
- | - 
TextAlign.left | 左对齐
TextAlign.center | 居中对齐
TextAlign.right | 右对齐

#### textDirection：文字方向

TextDirection 值 | 含义
- | -
TextDirection.ltr | 文字方向从左到右
TextDirection.rtl | 文字方向从右到左

#### overflow：文本的截断方式

TextOverflow 值 | 含义
- | - 
TextOverflow.ellipsis | 多余文本截断后以省略符“...”表示
TextOverflow.clip | 剪切多余文本，多余文本不显示
TextOverflow.fade | 溢出的部分会进行一个渐变消失的效果，上下渐变，非左右渐变。

#### style：设置文字样式

设置的文字样式，包括：文本颜色、下划线、行高、字体种类、字体粗细、字体是否倾斜等。通过 TextStyle 类的实例来赋值：

#### textScaleFactor VS fontSize

- fontSize可以精确指定字体大小，而textScaleFactor只能通过缩放比例来控制。
- textScaleFactor主要是用于系统字体大小设置改变时对Flutter应用字体进行全局调整，而fontSize通常用于单个文本，字体大小不会跟随系统字体大小变化。

``` dart
(new) TextStyle({
  bool inherit: true, 
  Color color, 
  double fontSize, 
  FontWeight fontWeight, 
  FontStyle fontStyle, 
  double letterSpacing, 
  double wordSpacing, 
  TextBaseline textBaseline, 
  double height, 
  Locale locale, 
  Paint foreground, 
  Paint background, 
  List<Shadow> shadows, 
  TextDecoration decoration, 
  Color decorationColor, 
  TextDecorationStyle decorationStyle, 
  String debugLabel, 
  String fontFamily, 
  List<String> fontFamilyFallback, 
  String package
}) → TextStyle
```

参数名字 | 参数类型	| 意义	| 必选 or 可选
- | - | - | -
inherit |	bool	| 是否继承父 Text 的样式，默认为 true；<br>如果为false，且样式没有设置具体的值，则采用默认值：白色、字体大小 10px、sans-serif 字体 |	可选
color	| Color	| 文字的颜色	| 可选
fontSize	| double	| 文字的大小	| 可选
fontWeight	| FontWeight	| 字体粗细	| 可选
fontStyle	| FontStyle	| 是否在字体中倾斜字形	| 可选
letterSpacing	| double	| 字母之间的间隔	| 可选
wordSpacing	| double	| 单词之间的间隔	| 可选
textBaseline | TextBaseline | 用于对齐文本的水平线	| 可选
height | double	| 文本的高度，<br>但它并不是一个绝对值，而是一个因子，具体的行高等于fontSize*height。	| 可选
locale | Locale	| 用于选择用户语言和格式设置首选项的标识符	| 可选
foreground	| Paint	| 文本的前景色	| 可选
background	| Paint	| 文本的背景色	| 可选
shadows	| List< ui.Shadow>	| 在文本下方绘制阴影	| 可选
decoration	| TextDecoration	| 文本的线条	| 可选
decorationColor	| Color	| TextDecoration 线条的颜色	| 可选
decorationStyle	| TextDecorationStyle	| TextDecoration 线条的样式	| 可选
debugLabel	| String	| 文本样式的描述<br>无实际用处	| 可读
fontFamily | String	| 用于设置使用哪种自定义字体	| 可读
fontFamilyFallback	| String	| 字体列表，当前面的字体找不到时，会在这个列表里依次查找	| 可读
package	| String	| 用于设置使用哪种自定义字体	| 可读

#### TextDecoration：文本的线条

TextDecoration 的值 | 含义
- | -
TextDecoration.underline | 下划线
TextDecoration.overline | 上划线
TextDecoration.lineThrough | 中划线
TextDecoration.none | 不划线

#### DecorationStyle：文本线条的种类

DecorationStyle 的值 | 含义
- | -
TextDecorationStyle.solid | 实线
TextDecorationStyle.dotted | 虚线（由点组成）
TextDecorationStyle.dashed | 虚线（必点要长）
TextDecorationStyle.wave | 波浪线
TextDecorationStyle.double | 两条线

### 2. Text 命名构造函数：Text.rich()

除了 text 的默认构造参数外，还有命名构造函数 Text.rich，用于创建多类型的文本。

``` dart
(new) Text.rich(
  TextSpan textSpan, {
    Key key, 
    TextStyle style, 
    StrutStyle strutStyle, 
    TextAlign textAlign, 
    TextDirection textDirection, 
    Locale locale, 
    bool softWrap, 
    TextOverflow overflow, 
    double textScaleFactor, 
    int maxLines, 
    String semanticsLabel
}) → Text

(new) TextSpan({
  TextStyle style, 
  String text,
  List<TextSpan> children, 
  GestureRecognizer recognizer
}) → TextSpan
```

demo 如下：
``` dart
Text.rich(
  TextSpan(
    children: [
      TextSpan(
        text: 'Center demo hahaha哈 哈 哈ahahah aahaha haa hahaha ahahaha aha hahaahahahaaha hahaahahahaahahah aahahahaahaha haahaha haa',
        style: TextStyle(
          color: Colors.red[300]
        )
      ),
      TextSpan(
        text: 'Center demo hahaha哈 哈 哈ahahah aahaha haa hahaha ahahaha aha hahaahahahaaha hahaahahahaahahah aahahahaahaha haahaha haa',
        style: TextStyle(
          color: Colors.green[300]
        )
      )
    ]
  )
)
```

### 3. RichText

[RichText](https://api.flutter.dev/flutter/widgets/RichText-class.html) 和 Text.rich 构造函数同作用，用来创建多样式文本。

继承关系如下：

    Object > Diagnosticable > DiagnosticableTree > Widget > RenderObjectWidget > LeafRenderObjectWidget > RichText

用法：
```dart
(new) RichText({
  Key key, 
  TextSpan text,(@required) 
  TextAlign textAlign: TextAlign.start, 
  TextDirection textDirection, 
  bool softWrap: true, 
  TextOverflow overflow: TextOverflow.clip, 
  double textScaleFactor: 1.0, 
  int maxLines, 
  Locale locale, 
  StrutStyle strutStyle
}) → RichText
```

#### TextSpan 的构造函数及参数说明

```
class TextSpan extends DiagnosticableTree {
  const TextSpan({
    this.style,
    this.text,
    this.children,
    this.recognizer,
  });
  ...
}
```

参数名字 | 参数类型	| 意义	| 必选 or 可选
- | - | - | - 
style	| TextStyle	| 文本样式	| 可选
text	| String	| 要显示的文字	| 可选
children	| List< TextSpan>	| 子 TextSpan	| 可选
recognizer | GestureRecognizer |	一个手势识别器，它将接收到达此文本范围的事件。 | 可选

RichText demo 如下：
``` dart
RichText(
  text: TextSpan(
    children: [
      TextSpan(
        text: 'Center demo hahaha哈 哈 哈ahahah aahaha haa hahaha ahahaha aha hahaahahahaaha hahaahahahaahahah aahahahaahaha haahaha haa',
        style: TextStyle(
          color: Colors.red[300]
        )
      ),
      TextSpan(
        text: 'Center demo hahaha哈 哈 哈ahahah aahaha haa hahaha ahahaha aha hahaahahahaaha hahaahahahaahahah aahahahaahaha haahaha haa',
        style: TextStyle(
          color: Colors.green[300]
        )
      )
    ]
  )
)
```

### 使用自定义字体的步骤

1. 在 pubspec.yaml 中声明，字体名、字体所在的本地目录、修饰字体（可选）。
2. 在 .dart 文件中使用即可。

``` yaml
# pubspec.yaml
fonts:
  - family: Roboto
    fonts:
      - asset: fonts/Roboto-Bold.ttf
        weight: 700
```

``` dart
child: Text(
  'Roboto',
  style: TextStyle(
    fontFamily: 'Roboto'
  )
)
```

即使 .ttf 文件路径没错，控制台仍可能会报错，重新 build APP 即可。

可参考：
- [fonts from packages](https://flutter.dev/docs/cookbook/design/fonts#from-packages)
- [flutter Text](https://api.flutter.dev/flutter/widgets/Text-class.html)
- [Text](https://book.flutterchina.club/chapter3/text.html)
