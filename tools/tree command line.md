## win
1. 下载 [Binaries zip](http://gnuwin32.sourceforge.net/packages/tree.htm) 文件。

2. 解压 zip，复制 bin/tree.exe 文件到 Git安装目录\usr\bin。

3. 在 git bash 中，使用 tree 命令即可。

## mac
使用 homebrew 安装 tree 命令行：`brew install tree`

## tree 命令部分参数

```
-a 显示所有文件和目录。(默认)
-F 在执行文件，目录(重要)，Socket，符号连接，管道名称名称，各自加上"*","/","=","@","|"号。
-s 列出文件/目录大小。
-D 显示文件/目录的更改时间。
-t 以文件和目录更改时间排序。
-d 仅列出目录名称。
-f 显示相对路径。
-i 不以阶梯状，列出文件/目录名称。

// 一般情况下：tree -F即可
```
