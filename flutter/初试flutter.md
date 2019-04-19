### 初识flutter

#### flutter 的优点：
  - 跨平台：支持Linux、Android、IOS，甚至嵌入式开发。
  - 原声用户界面：同rn类似使用原生控件来开发，体验更好，性能更加。
  - 开源免费。

#### 与其他主流框架对比：
  - `Cordova`：其使用网页的形式（html、css、js）开发移动UI，借助插件的形式开发移动应用。离底层硬件的距离最远。
  - `RN`：使用类原生view编译成底层原生view的方式实现UI。
  - `flutter`：使用了`Dart`语言,避免了RN的那种通过桥接器与Javascript通讯导致效率低下的问题。虽没使用原生控件来渲染UI，但效果却由于原生。并且采用了GPU渲染技术。

#### flutter的生态圈：
  - github：https://github.com/flutter/flutter
  - 生态圈：https://github.com/Solido/awesome-flutter
  - 官网：https://flutter.io/

#### 搭建flutter：
- 安装的文件
  + [Java SE Development Kit 8u191](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
  + [flutter-sdk（或者叫flutter的安装包） 0.9.4](https://flutter.io/docs/get-started/install)
  + [android studio](https://developer.android.com/studio/)
  + android sdk在android studio中集成了、android 模拟器需要手动create virtural device。
  + 在android studio中安装flutter插件。
- 注意
  + 在flutter目录下使用git bash设置源来更好地访问 Google 的服务。
    ```js
      export PUB_HOSTED_URL=https://pub.flutter-io.cn
      export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
    ```
  + 如果想让flutter命令在cmd上用，需要设置写环境变量到(/bin)目录 。
  + flutter doctor来诊断开发flutter环境是否完好。
- 参考：
  + [jd 前端开发](https://loveky.github.io/2018/07/04/flutter-first-experience/)
  + [技术胖win、mac](http://jspang.com/post/flutter1.html#toc-f3d) (推荐!)
  + [mac 系统搭建](https://segmentfault.com/a/1190000013624591)
  + [win安装及采坑](https://blog.csdn.net/jifashihan/article/details/80675267)
