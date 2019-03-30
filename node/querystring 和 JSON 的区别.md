# querystring 和 JSON 的区别

`querystring`: node 内部模块，用来解析/格式化查询字符串的。

`JSON`: js 内置类，用来实现 json 数据格式和字符串的互相转换。

## json => string

    const querystring = require('querystring')
    const obj = {
      name: 'I am Demo'
    }

    console.log(
      querystring.stringify(obj)  // 'name=I%20am%20Demo'
    )

    console.log(
      JSON.stringify(obj)         // '{"name":"I am Demo"}'
    )

## string => json

    const querystring = require('querystring')
    const str1 = 'name=I%20am%20Demo'
    const str2 = '{"name":"I am Demo"}'

    console.log(
      querystring.parse(str1)    // { name: 'I am Demo' }
    )

    console.log( 
      JSON.parse(str2)           // { name: 'I am Demo' }
    )

