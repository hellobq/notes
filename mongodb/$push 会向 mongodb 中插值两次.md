# $push 会向 mongodb 中插值两次

``` js
await User.updateOne({
  name
}, {
  $push: {
    views: {
      report_id: _id,
      view_date: new Date()
    }
  }
}, err => {
  if (err) handleErr(err)
})
```

以上代码执行后，mongodb 数据库会插值两条一摸一样json，这是因为**当使用了 promsie（或者 async/await）时，并且使用了回调参数**。

改成以下即可：

``` js
await User.updateOne({
  name
}, {
  $push: {
    views: {
      report_id: _id,
      view_date: new Date()
    }
  }
})
```

原文链接：[$push twice](https://stackoverflow.com/questions/49372428/mongoose-push-keeps-adding-two-entries)
