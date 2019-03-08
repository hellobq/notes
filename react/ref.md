# ref

虽然React官方力荐数据驱动UI，但是有时确实需要获取真实dom对象，比如：焦点问题、图片加载完成后获取宽高、媒体控制等。

#### 1. 通过回调函数

```js
// jsx中
<div ref={div => this.box = div}></div>

// 使用时
this.box
```

#### 2. 通过React.createRef()

```js
constructor (props) {
  super(props)
  this.box = React.createRef()
}

// jsx中
<div ref={this.box}></div>

// 使用时
this.box.current
```

#### 3. 高阶组件中获取原组件 ref

通过调用原组件的ref回调函数。

``` js
// 高阶组件
const withLoading = WrapperComponent => props => {
  let getInput = null
  const handleClick = e => {
    console.log(getInput.focus())
  }
  return (
    <div>
      <WrapperComponent {...props} inputRef={input => getInput = input}/>
      <button onClick={handleClick}>点击获取焦点</button>
    </div>
  )
}


// 原始组件
class Test extends Component {
  inputRef = null
  componentDidMount () {
    this.props.inputRef(this.inputRef)
  }
  render () {
    return (
      <input type="text" ref={input => this.inputRef = input}/>
    )
  }
}

export default withLoading(Test)
```

#### 注意事项：

如果用在h5标签上，是获取dom节点；用在子组件上就是获取子组件实例。

在 componentDidMount ~ componentDidUpdate 期间有作用。当重新渲染后，oldRef清除，newRef更新。

函数组件没有refs。
