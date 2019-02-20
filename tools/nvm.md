# nvm

Node包管理工具。

## win下安装nvm：

下载 nvm-setup.zip https://github.com/coreybutler/nvm-windows/releases

安装nvm时，可以设置nvm的安装位置，node默认安装位置是 C:\Program Files\nodejs，并且会把它放到path中。

在nvm的安装目录下设置setting.txt文件，增加以下两项，使得用淘宝源下载node和npm:
- node_mirror: https://npm.taobao.org/mirrors/node/
- npm_mirror: https://npm.taobao.org/mirrors/npm/

## nvm 常用命令
- 查看nvm常用命令，nvm
- 安装某个版本的node: nvm install 8.11.3
- 查看已安装的node版本: nvm ls
- 使用某个版本的node: nvm use 8.11.3
- 卸载某个版本的node: nvm uninstall 8.11.3

## 相关链接：
- https://segmentfault.com/a/1190000015962368
- https://segmentfault.com/a/1190000011510188
