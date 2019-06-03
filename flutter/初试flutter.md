### 初识flutter

Google 开源的跨平台 UI 框架。

#### flutter 的优点：
  - 跨平台：不用像 RN 一样担心适配，默认支持安卓和 IOS，经扩展后还支持 PC 端（windows、linux、macOS）、web 端。
  - 高性能：渲染帧率达到 60FPS，通过 JNI 桥接 Native，Flutter 和 Native 之间的交互损耗很低。
  - UI 部件很丰富，Flutter 内置众多精美的 Material Design(Android 风格)和Cupertino(IOS 风格)的小部件。直接使用、方便组合。
  - 学习成本低。屏蔽了底层地 实现，用户只需要学习 Flutter 这个框架即可。
  - 开发效率很高。一份代码就能构建出 Android 和 IOS 两个平台的 APP，这才是真正做到一次书写，多平台运行。
  - ......

#### 与其他主流框架对比：
  - `Cordova/Hybird`：其使用网页的形式（html、css、js）开发移动 UI，借助插件的形式开发移动应用。离底层硬件的距离最远。WebView 的渲染性能和 javascript 的解析效率比 Native 很差。
  - `RN/Weex`：使用类原生 view 编译成底层原生 view 的方式实现 UI，使用 js 引擎运行 js 代码。
  - `flutter`：使用了 `Dart` 语言,避免了RN的那种通过桥接器与Javascript通讯导致效率低下的问题。虽没使用原生控件来渲染UI，但效果却由于原生。并且采用了 GPU 渲染技术。在跨平台和性能上都更高一筹。

#### flutter的生态圈：
  - github：https://github.com/flutter/flutter
  - 生态圈：https://github.com/Solido/awesome-flutter
  - 官网：https://flutter.io/
  - Flutter 所有 widget: https://api.flutter.dev/flutter/widgets/widgets-library.html

#### 搭建flutter：

见掘金小册
