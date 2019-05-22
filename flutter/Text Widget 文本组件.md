## Text Widget 文本组件



maxLines: 设置最多显示的行数。

overflow: 用来设置文本溢出时的显示方式
- clip：直接切断，剩下的文字就没有了，感觉不太友好，体验性不好。
- ellipsis: 在后边显示省略号，体验性较好，这个在工作中经常使用。
- fade: 溢出的部分会进行一个渐变消失的效果，上下渐变，非左右渐变。

style：样式属性
- fontSize: 字体大小 
- color: 字体颜色。Color.fromARGB(255, 255, 0, 0)ARGB颜色值,也可以使用Color(0xffff0000)十六进制颜色码
或者使用Colors类中封装的颜色：Colors.purple
- decoration: 下划线 lineThrough 删除线，underline下划线，overline上划线 ,none默认
- decorationStyle: 装饰样式 solid实线，dashed虚线，dotted虚线（由点组成）,double两行，wavy波浪线
- decorationColor: 装饰颜色 支持ARGB颜色值/十六进制

其他相关属性：https://docs.flutter.io/flutter/painting/TextStyle-class.html
