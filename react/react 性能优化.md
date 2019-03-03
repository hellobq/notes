# react 性能优化

性能优化：防止组件无谓render。父组件重新render，子组件就会紧跟着render，如果子组件从父组件得到的数据没发生更改，却也重新render，就造成了性能损耗。



#### 1. 通过生命周期方法 shouldComponentUpdate

``` js
// 父组件
class App extends Component {
  state = {
    n: 0,
    num: 0
  }
  handleClick = () => {
    this.setState(state => ({
      n: state.n + 1
    }))
  }
  render () {
    return (
      <div>
        <button onClick={this.handleClick}>点击</button>
        <Test num={this.state.num}/>
      </div>
    )
  }
}


// 子组件
class Test extends Component {
  // 当props.num 改变了，才重新渲染
  shouldComponentUpdate (nextProps, nextStates) {
    return nextProps.num !== this.props.num
  }
  render () {
    console.log("rerender")
    return (
      <p>test</p>
    )
  }
}
```


#### 2. 每个子组件都这样写一次 shouldComponentUpdate 太麻烦了，因此对于 `类组件` 来说，直接使用 `PureComponent` 即可：

``` js
class Test extends PureComponent {
  render () {
    console.log("rerender")
    return (
      <p>test</p>
    )
  }
}

```



#### 3. 对于props下的基本数据类型，可以通过 `!== 或者 PureComponent` 来判断是否改变。

#### 但是：对于引用类型（数组、对象）是行不通的，PureComponent仅是浅比较，此时不得不借用 immutable.js 的 is 方法，来判断这个引用类型的值是否发生了变化。

> 浅比较：只是比较内存地址，如果内存地址没变，里边的值变了，PureComponent / React.Memo 也是当做 props 没变。

``` js
import { fromJS, is } from 'immutable'

shouldComponentUpdate (nextProps, nextStates) {
  return !is(fromJS(this.props.obj), fromJS(nextProps))
}
```

