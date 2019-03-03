# hooks

React16.8 引入原因：

#### 很难重用有状态的组件逻辑

React没有提供将可重用行为“附加”到组件的方法（例如，将其连接到商店）。如果您已经使用React一段时间，您可能熟悉渲染props和高阶组件等试图解决此问题的模式。但是这些模式要求您在使用它们时重构组件，这可能很麻烦并且使代码更难以遵循。如果你看一下React DevTools中典型的React应用程序，你可能会发现一个由包含提供者，消费者，高阶组件，渲染props和其他抽象层的组件组成的“包装器地狱”。虽然我们可以在DevTools中过滤掉它们，但这指出了一个更深层次的基本问题：React需要一个更好的原语来共享有状态逻辑。

使用Hooks，您可以从组件中提取有状态逻辑，以便可以独立测试并重复使用。钩子允许您在不更改组件层次结构的情况下重用有状态逻辑。这样可以轻松地在许多组件之间或与社区共享Hook。

#### 复杂点的组件很难被理解

复杂的组件变得难以理解
我们经常不得不维护从简单开始的组件，但却变成了无法管理的状态逻辑和副作用。每个生命周期方法通常包含不相关逻辑的混合。例如，组件可能会在componentDidMount和componentDidUpdate中执行一些数据提取。但是，相同的componentDidMount方法可能还包含一些设置事件侦听器的无关逻辑，并在componentWillUnmount中执行清理。一起更改的相互关联的代码被拆分，但完全不相关的代码最终组合在一个方法中。这使得引入错误和不一致变得太容易了。

在许多情况下，不可能将这些组件分解为较小的组件，因为有状态逻辑遍布整个地方。测试它们也很困难。这是许多人更喜欢将React与单独的状态管理库相结合的原因之一。但是，这通常会引入太多的抽象，要求您在不同的文件之间跳转，并使重用组件更加困难。

为了解决这个问题，**Hooks允许您根据相关的部分（例如设置订阅或获取数据）将一个组件拆分为较小的函数，而不是基于生命周期方法强制拆分**。您还可以选择使用reducer管理组件的本地状态，以使其更具可预测性。

#### 让人头昏的class

除了使代码重用和代码组织更加困难之外，我们发现类可能是学习React的一大障碍。您必须了解它在JavaScript中是如何工作的，这与它在大多数语言中的工作方式有很大不同。您必须记住绑定事件处理程序。没有不稳定的语法提议，代码非常冗长。人们可以很好地理解props，状态和自上而下的数据流，但仍然很难与类斗争。 React中的函数和类组件之间的区别以及何时使用每个组件导致即使在经验丰富的React开发人员之间也存在分歧。

## state hook

通过数组结构，给组件添加本地状态、更改本地状态的方法。

- 初始参数，仅在第一次渲染使用。
- 修改state, 该方法并不会合并新老状态，而是直接把新状态替换掉老状态。
- 修改state，this.setState必须要传递整个state，而useState必须传递整个state。

#### 定义多个本地状态

各个本地状态可以是不同类型的。

``` js
function ExampleWithManyStates() {
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

## effect hook

在组件中数据获取、事件注册/注销、订阅/取消订阅、更改DOM都属于副作用。通由effect hool来管理。它代替了类组件中的componentDidMount/compoenntDidUpdate/componentWillUnmount这些钩子，统一了API。

- 每当DOM更新后，会执行一遍effect hook。
- effect hook第一个参数的返回值（通常是函数），用来清理副作用（比如取消订阅/注销事件...）。
- effect hook第二个参数，是个数组。如果其中的项更改，才会重新执行effect hook；如果是个空数组，则effect hooks只会在组件创建和卸载时执行。

## hook 的规则

- 只能在顶层调用hooks。不能在条件/循环/嵌套函数中执行。
- 只能在react函数组件中定义，不能在常规函数中使用。

可使用 [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks) 检测hooks的书写规则。

## 使用hooks的直观好处

- 不用this
- 不用生命周期方法
- 有状态的组建逻辑很容易重用


## 其他hook：

- useContext允许你订阅React上下文而不用引入嵌套。
- useReducer允许你使用reducer管理复杂组件的本地s

## 防止函数组件无谓render

React.memo或者useMemo，作用原理和PureComponent类似。
