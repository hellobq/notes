# mysql 起步

下载 mysql: https://dev.mysql.com/downloads/repo/yum/

下载完成后，解压；在 mysql 安装路径下，新建 mysql 配置文件 --- my.ini：

    [mysql]
    # 设置mysql客户端默认字符集
    default-character-set=utf8
    
    [mysqld]
    # 设置3306端口
    port = 3306

    # 设置mysql的安装目录
    basedir=D:\mysql-8.0.15-winx64
    # 设置 mysql数据库的数据的存放目录，MySQL 8+ 不需要以下配置，系统自己生成即可，否则有可能报错
    # datadir=D:\mysql-8.0.15-winx64\data

    # 允许最大连接数
    max_connections=20
    # 服务端使用的字符集默认为8比特编码的latin1字符集

    character-set-server=utf8
    # 创建新表时将使用的默认存储引擎
    default-storage-engine=INNODB

启动本地 mysql: 

&nbsp;&nbsp;&nbsp;&nbsp;1. 用管理员身份打开 cmd，切换到 mysql 安装目录下，初始化 mysql: `mysqld --initialize --console` (此时会在安装目录下自动产生 data 目录)

&nbsp;&nbsp;&nbsp;&nbsp;2. 输入 mysql 安装命令: `mysqld install`

&nbsp;&nbsp;&nbsp;&nbsp;3. 启动 mysql: `net start mysql`

进入 mysql 命令行：

&nbsp;&nbsp;&nbsp;&nbsp;1. 需要登陆 mysql: `mysql -u root -p`，再输入密码即可。

&nbsp;&nbsp;&nbsp;&nbsp;2. 接下来就可写 mysql 代码了。

Navicat: mysql 的可视化工具。

错误集锦：
- [mysql Install/Remove of the Service Denied ! ](https://blog.csdn.net/lxpbs8851/article/details/14161935)
- [win10安装mysql报错——项识别为 cmdlet、函数、脚 本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确，然后再试一次。](https://blog.csdn.net/qq_35685189/article/details/83751050)
- [cmd中输入net start mysql 提示：服务名无效或者MySQL正在启动 MySQL无法启动。](https://blog.csdn.net/ermaner666/article/details/79096939)
- [MySQL无法启动 服务没有报告任何错误。](https://blog.csdn.net/u013294097/article/details/79814274)
- [Navicat for Mysql报错1251连接不成功Mysql。](https://blog.csdn.net/wshxhghsjjsn/article/details/80459542)

学习连接：
- [菜鸟教程 mysql](http://www.runoob.com/mysql/mysql-install.html)
