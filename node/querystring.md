# querystring

解析和格式化 url 中 query 参数(查询字符串)。常用方法有：querystring.parse() / querystring.stringfy()

## querystring.parse()

将查询字符串解析并转换成对象。

    const querystring = require('querystring')
    querystring.parse('foo=b%20ar&abc=xyz&abc=123')  
    // { foo: 'b ar', abc: [ 'xyz', '123' ] }
    
## querystring.stringfy()

将对象解析并转换成查询字符串。
    
    const querystring = require('querystring')
    querystring.stringfy( { foo: 'ba>r', baz: ['qux', 'quux'], corge: '' } )
    // 'foo=ba%3Er&baz=qux&baz=quux&corge='

## querystring 和 JSON 的区别

`querystring`: node 内部模块，用来实现 `url 中的 query 参数` 和 json 数据格式的互相转换。

`JSON`: js 内置类，用来实现 json 数据格式和字符串的互相转换。

#### json => string

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

#### string => json

    const querystring = require('querystring')
    const str1 = 'name=I%20am%20Demo'
    const str2 = '{"name":"I am Demo"}'

    console.log(
      querystring.parse(str1)    // { name: 'I am Demo' }
    )

    console.log( 
      JSON.parse(str2)           // { name: 'I am Demo' }
    )


