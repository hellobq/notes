# 简介 nginx

一个轻量的 `http` 服务器，采取：事件驱动、异步非阻塞的方式，和 `Node` 类似，具有极好的 `I/O` 性能
，主要用于服务器端的反向代理和负载均衡。

## nginx 的优点

1. 支持高并发量。最大达到5万以上的并发连接。

2. 内存消耗少：在主流的服务器中 `Nginx` 目前是内存消耗最小的了，比如我们用 `Nginx + PHP`，在3万并发链接下，开启10个 `Nginx` 进程消耗150M内存。

3. 开源、免费。可用作商业化。

4. ...

## nginx 相关命令（CentOS 环境下）

查看 nginx 相关文件路径：`rpm -ql nginx`，rpm 是linux的rpm包管理工具，-q 代表询问模式，-l 代表返回列表，这样我们就可以找到nginx的所有安装位置了。

启动 nginx： 
- 在 CentOS7.4 以上，直接使用 `nginx` 即可启动 nginx。
- 使用 systemctl 命令启动：`systemctl start nginx.service`

查询与 nginx  有关的服务：`ps aux | grep nginx`

停止 nginx 服务：
- 立即停止服务：`nginx -s stop`
- 从容停止服务：`nginx -s quit`
- 直接 kill 掉进程：`killall nginx`
- systemctl 停止：`systemctl stop nginx.service`

重启 nginx 服务：`nginx -s reload`

查看端口号：`netstat -tlnp`
