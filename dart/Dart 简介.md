# Dart 简介

Dart 是由 `Google` 开发的开源语言，主要用于：

- 开发跨终端的 `app`。
- 创建 `web` 但也应用。
- 创建命令行工具和服务器。

Dart 的特性：变量是动态、可选的，有类单继承和多接口，还支持多线程。

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
