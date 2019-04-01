# 操作 mysql 数据库

需要使用 [mysql](https://github.com/mysqljs/mysql) 这个模块来操作 mysql 的 js 库。

``` js
const mysql = require('mysql')

// 用 mysql 模块，连接本地开启的 mysql 数据库
const db = mysql.createConnection({   // 可能会使用 createPool 代替 createConnection，有个连接池的概念
  host: 'localhost',
  port: 3306,
  user: 'root',
  password: 'root',
  database: 'test' 
})

const username = 'demo'
const password = '123456'

db.query(`INSERT INTO user (username, password) VALUES ('${username}', '${password}')`, (err, data) => {
  if (err) {
    console.error(err)
  } else {
    console.log(data)
  }
})

db.query(`SELECT * FROM user`, (err, data) => {
  if (err) {
    console.error(err)
  } else {
    console.log(data)
  }
})
```
