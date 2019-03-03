# prop-types

js是弱类型语言，在react组件中，通过引入 `prop-types` 第三方库检查管道 prop 类型，防止属性间传值类型出错。

当然，也有使用flow、TypeScripts对整个应用进行类型检查，这是另一方面了。

## PropTypes类型检查步骤：
  
#### 1. 由于从React v15.5起把 `prop-types` 剥离了，所以需要手动安装`prop-types` 这个库。
  
**注意**：在create-react-app脚手架中自带prop-types，直接使用引用即可。

```js
  import PropTypes from 'prop-types'
```

#### 2. 如果校验MyComponent的content属性是否为String类型，可以这样写：

```js
  MyComponent.propTypes = {  /* 注意这里的p是小写*/
    content: PropTypes.string
  }
```

#### 3. 使用`isRequired`规定父组件必须传递。因为propTypes只会对传过来的属性来类型检测，如果父组件没传该属性，即使写了类型检测也没用。

```js
  MyComponent.propTypes = {
    content: PropTypes.string.isRequired
  }
```

#### 4. 如果组件必须要某个属性，但是父组件并不确保可以传过去，为了避免由isRequired带来的警告，可以给该属性来个默认值。eg:

```js
  MyComponent.defaultProps = {
    content: 'this is default props!'
  }
```

## propTypes有哪些？
下面列举常用的类型：[所有的类型?](https://react.docschina.org/docs/typechecking-with-proptypes.html)

```js
  // JS 原生类型
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,  
  optionalFunc: PropTypes.func,  
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,

  // 某一种类型
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number
  ]),

  // 某一特定值
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),

  // 一个指定元素类型的数组
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

  // 一个指定类型的对象
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),
  
  // 任意类型的数据
  requiredAny: PropTypes.any.isRequired,
```

## 注意事项：

- `prop-types` 仅在开发环境中校验，生产环境则没有。
- `PropTypes.func、PropTypes.bool`而不是`PropTypes.Function、PropTypes.boolean` 这是因为function和boolean在js中是关键词。
