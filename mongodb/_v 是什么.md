# __v 是什么 ？

每次创建 document 时，其中总会自动添加属性 `_v`。`__v` 是 mongodb 用来标识这个 document 创建的版本，是不是刚创建的。

可以显示地设置，在创建 document 时，不加 `__v` 属性：

``` js
const UserSchema = new Schema({
  name: {
    type: String,
    unique: true
  },
  pwd: String,
  regDate: Date,
  comments: [{
    type: Schema.Types.ObjectId,
    ref: 'Comment'
  }],
  collections: [{
    type: Schema.Types.ObjectId,
    ref: 'Report'
  }], 
  views: [{
    report_id: {
      type: Schema.Types.ObjectId,
      ref: 'Report'
    },
    view_date: Date
  }]
}, {
  collection: 'users',
  versionKey: false
})
```

