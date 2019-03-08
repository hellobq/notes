# stream

[stream](http://nodejs.cn/api/stream.html#stream_stream) 继承 [EventEmitter](http://nodejs.cn/api/events.html#events_class_eventemitter)，stream 用来创建新类型的流实例，实际开发中主要使用流实例。例如：[http 的请求](http://nodejs.cn/api/http.html#http_class_http_incomingmessage)、[process.stdout](http://nodejs.cn/api/process.html#process_process_stdout)等。

## 流的类型

#### 1. 可写流 Writeable。如：[fs.createWriteStream()](http://nodejs.cn/api/fs.html#fs_fs_createwritestream_path_options)

#### 2. 可读流 Readable。如：[fs.createReadStream()](http://nodejs.cn/api/fs.html#fs_fs_createreadstream_path_options)

#### 3. 可读可写流 Duplex。如：[net.Scoket()](http://nodejs.cn/api/net.html#net_class_net_socket)

#### 4. 在读写过程中，可转换数据的流 Transform。如：[zlib.createGzip()]()


