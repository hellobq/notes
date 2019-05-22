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

#### 1.1 textAlign

当父部件宽度大于 text 长度时，textAlign 用来设置字体对齐方式。

TextAlign: left(左对齐)、center（居中对齐）、right（右对齐）。

#### 1.2 softWrap

text 中含有英文单词，如果当前宽度展示不了该英文单词，会自动换行。

#### 1.3 maxLines

设置最大行数，超出最大行数将不再显示。需要注意的是，英文字母如果很长的话，即使设置了最大行数，它也不会自动截断，此时设置 softWrap: false 拒绝英文单词自动换行即可。

#### 1.4 overflow

用来设置文本溢出时的显示方式

- clip：直接切断，剩下的文字就没有了，感觉不太友好，体验性不好。
- ellipsis: 在后边显示省略号，体验性较好，这个在工作中经常使用。
- fade: 溢出的部分会进行一个渐变消失的效果，上下渐变，非左右渐变。

#### 1.5 style

设置文字样式，通过 TextStyle 类的实例来赋值：

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

- fontSize: 字体大小 
- color: 字体颜色
- fontWeight: 字体粗细
- fontStyle: 字体倾斜
- letterSpacing: 字母间隔
- wordSpacing: 单词间隔
- decoration: 文本线条 lineThrough 删除线，underline下划线，overline上划线 ,none默认
- decorationStyle: 线条种类 solid实线，dashed虚线，dotted虚线（由点组成）,double两行，wavy波浪线
- color: 文本颜色
- height: 文本行高。1.2 等于字体 fontSize 的 1.2 倍

### 2. Text.rich()

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


demo 如下：
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
