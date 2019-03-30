# fs

[fs](http://nodejs.cn/api/fs.html#fs_file_system) 是 node 的内置文件模块，包括同步/异步。

## fs.Stats类

[fs.Stats](http://nodejs.cn/api/fs.html#fs_class_fs_stats)这个类没什么用，有用的是fs.Stats实例下有关文件（夹）的方法/属性，但是stats实例通常不是有fs.Stats这个类创建的，这个实例通常位于其他fs方法的回调参数上。

且看stats实例的方法/属性：

``` js
stats.isFile(): 是否是文件

stats.isDirectory(): 是否是目录。

stats.size: 文件大小，以字节为单位。

// 等等...

```

## fs.stat()

异步地检查文件是否存在。语法为：

``` js
fs.stat(path[, opts], callback)

// 文件不存在，err不为空。文件存在，返回文件相关信息stats
callback: function(err, stats)  

```

## fs.statSync()

[fs.statSync](http://nodejs.cn/api/fs.html#fs_fs_statsync_path_options) 同步地检查文件是否存在。如果文件存在，返回stats对象；如果不存在就要报错了，需要try..catch。语法为：

``` js
fs.statSync(path[, opts])

try {
  const stats = fs.statSync('./demo.txt')
} catch (e) {
  console.error('文件不存在...')
}

```

## fs.mkdir()

[fs.mkdir](fs_fs_mkdir_path_options_callback)异步创建文件目录，有两个坑：

- 创建目录，是以C盘根目录开始的，不是当前目录。需要加__dirname
- 目录只能一层层创建，不能一下创建嵌套目录。

语法如下：

``` js
fs.mkdir(path[, opts], callback)

callback: function(err)

fs.mkdir(__dirname + '/tmp', err => {
  if (err) {
    console.error('创建目录出错...')
  }
  // ...
})

```

## fs.mkdirSync()

[fs.mkdirSync]同步地创建目录。语法如下：

``` js
fs.mkdirSync(path[, opts])

try {
  const dir = fs.mkdirSync(__dirname + '/1')

  console.log(dir)
} catch (e) {
  console.error('创建目录失败...')
}

```

## fs.rmdir()

异步删除目录，如果没这个目录，则删除失败。语法如下：

``` js
fs.rmdir((path, callback))

fs.rmdir(__dirname + '/tmp', err => {
  if (err) {
    console.log('找不到当前目录，删除出错...')
  }

  // ...
})

```

## fs.rmdirSync()

同步删除目录。语法如下：

``` js
fs.rmdirSync(path)

try {
  fs.rmdirSync(__dirname + '/tmp')
  // ...
} catch (e) {
  console.error('目录不存在，删除失败...')
}

```

## fs.unlink()

异步地删除文件。语法如下：

``` js
fs.unlink(path, callback)

callback: function (err)

fs.unlink(__dirname + '/demo.txt', err => {
  console.error('未找到文件，不能删除...')
})

```

## fs.unlinkSync()

同步地删除文件。语法如下：

``` js
fs.unlinkSync(path)

try {
  fs.unlinkSync(__dirname + '/demo.txt')
} catch (e) {
  console.error('未找到文件，不能删除...')
}

```

## fs.writeFile()

异步地将数据写在文件内，如果文件存在则覆盖原来的内容。语法如下：

    fs.writeFile(path, data[, opts], callback)

    opts: 对象。有个选项encoding，规定以什么编码方式写文件内容。默认"utf8"，如果是data是Buffer，则忽略encoding选项。

    fs.writeFile(__dirname + '/demo.txt', 'hjsa 婚纱', err => {
      if (err) {
        console.log('文件不存在，不能写入...')
      }
    })

## fs.writeFileSync()

同步将数据写入文件，如果文件存在则覆盖。需要try....catch。语法如下：

``` js
fs.writeFileSync(path, data[, opts])

try {
  fs.writeFileSync(__dirname + '/demo.txt', 'lalalal')
} catch (e) {
  console.log('文件不存在，不能写入...')
}
```

## fs.appendFile() / fs.appendFileSync()

参数格式同上两者，异步/同步地向文件中追加内容，而不是直接覆盖。

## fs.readdir()

异步地读目录，语法如下：

    fs.readdir(path[, opts], callback)

    callback: funciton (err, files)

    fs.readdir(__dirname + '/src', (err, files) => {
      if (err) {
        console.error('目录不存在...')
      }
      console.log('文件名（可能包含文件夹）组成的数组为：', files)
    })

    // 文件夹的名字也会在 files 数组内。当前目录没子文件的话，files为空数组。

## fs.readdirSync()

同步地读目录内容，语法如下：

    fs.readdirSync(path[,opts])

    try {
      const files = fs.readdirSync(__dirname + '/src')
      console.log('文件名（可能包含文件夹）组成的数组为：', files)
    } catch(e) {
      console.error('目录不存在...')
    }

## fs.readFile()

异步地读文件的全部内容，语法如下：

    fs.readFile(path[, opts], callback)

    callback: function (err, data<string|Buffer>)
    
    // opts.encoding: 默认为 null，data 为 Buffer；指定了则返回 string

    fs.readFile(__dirname + '/demo.txt', { encoding: 'utf8' },(err, data) => {
      if (err) {
        console.error('读文件出错...')
      }
      // ...
    })

## fs.readFileSync()

同步地读取文件中的数据，语法如下：

    fs.readFileSync(path[, opts]) 返回string|Buffer

    try {
      const content = fs.readFileSync(__dirname + '/demo.txt')
      // ...
    } catch (e) {
      console.error('未找到文件，读取失败...')
    }

## fs.rename()

异步地给文件命名，如果命名后的文件名已存在，那么将覆盖。语法如下：

``` js
fs.rename(oldPath, newPath, callback)

callback: function (errr)

fs.rename(__dirname + '/demo.txt', __dirname + '/haha.txt', err => {
  if (err) {
    console.log('未找到原文件，不能命名...')
  }

  // ...
})

```

## fs.renameSync()

同步地给文件命名。语法如下：

``` js
fs.renameFileSync(oldPath, newPath)

try {
  fs.renameSync(__dirname + '/demo.xtt', __dirname + '/haha.txt')
} catch (e) {
  console.error('未找到原文件，不能命名...')
}

```

## 案列：遍历某个文件夹下的所有文件及其子文件夹

``` js

const getAllFileName = pathName => {
  fs.readdir(pathName, (err, files) => {
    files.forEach(Name => {
      fs.stat(pathName + '/' + Name, (err, stats) => {
        if (stats.isDirectory()) {
          getAllFileName(pathName + '/' + Name)
        } else {
          console.log(pathName + '/' + Name)
        }
      })
    })
  })
}

getAllFileName(__dirname + '/src')
```

## fs流

实现大文件的迁移。

## fs.createReadStream()

[fs.createReadStream](http://nodejs.cn/api/fs.html#fs_fs_createreadstream_path_options) 创建一个读取文件的流，语法如下：

``` js
fs.createReadStream(path[, opts])

const readFileStream = fs.createReadStream(__dirname + '/demo.txt')
let content = ''

readFileStream.on('data', chunk => {
  console.log(`接收${chunk}字节的数据`)
  content += chunk
})

readFileStream.on('end', () => {
  console.log('内容为：', content)
})

readStream.on('error', err => {
    console.log(err)
})
```

## fs.createWriteStream()

[fs.createWriteStream](http://nodejs.cn/api/fs.html#fs_fs_createreadstream_path_options) 创建写入流，语法如下：

``` js
fs.createWriteStream(path[, opts])

const writeStream = fs.createWriteStream(__dirname + '/hello.txt')

// 把data按流方式写入
writeStream.write(data[, opts])

// 完成写入
writeStream.on('finish', () => console.log('写入完成...'))
```

把fs.md文件读到hello.md文件内：

``` js
const fs = require('fs')

const readFileStream = fs.createReadStream(__dirname + '/fs.md')
let content = ''

readFileStream.on('data', chunk => {
  content += chunk
})

readFileStream.on('end', () => {
  const writeStream = fs.createWriteStream(__dirname + '/hello.md')
  writeStream.write(content, 'utf8')
  writeStream.end()
})

```
