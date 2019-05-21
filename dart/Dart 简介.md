# Dart 简介

Dart 是由 `Google` 开发的开源语言，主要用于：

- 开发跨终端的 `app`。
- 创建 `web`应用。
- 创建命令行工具和服务器。

# Dart 语言优势

- Dart 中所有语言都是对象。均继承 Object，对象的默认值都是 null。
- 支持静态编译（JIT）、静态编译（AOT）。
- 数据类型支持强类型、动态类型（var、dynamic）。
- 具有异步编程能力。

Dart 的特性：动态、类型的声明是可选的，有类单继承和多接口，还支持多线程。

# Dart 全栈式语言

虽然 Dart 可用于开发移动端、pc 端、WEB、服务器开发，是一门全栈式语言，但是使用的框架是不一样的。

- Dart for the flutter 在 Flutter 上使用的 Dart 框架。
- Dart for the web 在 Web 上使用的 Dart 框架。
- Server-side Dart 在服务端使用的 Dart 框架。

# 在vscode编写dart

[下载 dart SDK](http://www.gekorm.com/dart-windows)，SDK 用来来解析并执行 dart 文件。

等待安装完成后，dart SDK/bin 会自动加载电脑的环境变量内。

在控制台输入 dart --version，即可输出 dart SDK 版本。

安装 vscode 中有关 dart 插件 --- dart。

编写 demo.dart 文件：

``` dart
// Define a function.
printNumber(num aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
main() {
  var number = 42; // Declare and initialize a variable.
  printNumber(number); // Call a function.
}
```

控制台执行：dart demo.dart，即可输出 dart 文件的执行结果。

学习 `Dart` 链接：

- [Dart 内容导航中文版](http://dart.goodev.org/guides/language/language-tour#exceptions%E5%BC%82%E5%B8%B8)
- [编程字典](http://codingdict.com/article/21933)
