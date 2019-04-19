### 在vscode中写flutter

#### 安装插件
 - 安装flutter插件。安装其同时，vscode会自动安装dart插件。

#### 步骤：
  - 使用vscode结合虚拟机的方式来开发。（使用vscode代替android studio，省性能）
  - 在桌面创建.bat文件，输入以下内容：
    + `C:\Users\hello\AppData\Local\Android\Sdk\emulator\emulator.exe -netdelay none -netspeed full -avd Nexus_5X_API_28`
    + 描述：以上路径是使用android studio创建过的虚拟机的目录，并加些网络无延迟设置，最后是虚拟机名称（不允许有空格，所以用_连接的）。
  - 初次打开.bat文件，需要使用管理员身份打开。
  - 在项目根目录敲flutter run即可。

#### 代码调试
  - 当代码修改时，在git bash里敲r键即可重新加载界面。（还有另外一种方式：在当前.dart文件中使用调试工具，按下开始即可实现热更新）。
  - 按p显示布局的网格。
  - 按o切换IOS和Android环境下的布局。
