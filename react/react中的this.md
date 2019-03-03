# react 中的 this 绑定

为了正确的绑定 react 类组件实例，一开始不得不手动绑定 this：

``` js
class App extends Component {

  handleClick () {
    console.log(this);  // App 实例
  }

  render (
    <button onClick={this.handleClick.bind(this)}>
      click
    </button>
  )
}
```

但是，每次click事件触发都会手动绑定this，有一定的性能损耗，所以，第二种方式：在 constructor 钩子里声明函数 handleClick 绑定的 this 值：

``` js
class App extends Component {

  constructor (props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick () {
    console.log(this);
  }

  render () {
    return (
      <button onClick={this.handleClick}>
        click
      </button>
    )
  }
}
```

但是，额外的问题是：多个事件句柄岂不是需要在 constructor 注册多次？通过箭头函数解决！（力推）

``` js
class App extends Component {

  handleClick = () => {
    console.log(this);  // App 实例
  }

  render () {
    return (
      <div className={styles.box}>
        <button onClick={this.handleClick}>点击</button>
      </div>
    )
  }
}
```
