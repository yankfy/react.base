# Hello World
## React.createClass
它的作用是注册一个组件类HelloComponent,这个组件类只包含一个render函数，该函数通过调用React.createElement实现了以下HTML内容：
```html
<h1>Hello world</h1>
```
## ReactDOM.render()
ReactDOM.render是React的最基本方法，用于将模板转为HTML语言，并插入指定的DOM节点。

# JSX语法
## JSX中的表达式
JSX是支持表达式的，你只要使用{}括号，就可以使用表达式了。
```js
var HelloComponent =React.createClass({
    render:function(){
        return <h1>Hello {this.props.name?this.props.name:'world'}</h1>;
    }
});
 
ReactDOM.render(
    <HelloComponent name="jspang"/>,
    document.getElementById('reactContainer')
)
```
## JSX上的数组输出
```js
let arr=[
    <h1 key="1">Hello world!</h1>,
    <h2 key="2"> React is awesome</h2>
];
ReactDOM.render(
<div>{arr}</div>, document.getElementById('reactContainer') )
```
# React组件
## state成员
*程序中需要注意的点*
 
- getInitialState函数必须有返回值，可以是null,false,一个对象。
- 访问state数据的方法是”this.state.属性名”。
- 变量用{}包裹，不需要再加双引号。
## props成员
*props与state的区别*
props不能被其所在的组件修改，从父组件传递进来的属性不会在组件内部更改；state只能在所在组件内部更改，或在外部调用setState函数对状态进行间接修改。
## 生命周期
过程中涉及三个主要的动作术语：

- mounting:表示正在挂接虚拟DOM到真实DOM。
- updating:表示正在被重新渲染。
- unmounting:表示正在将虚拟DOM移除真实DOM。

每个动作术语提供两个函数：

- componentWillMount()
- componentDidMount()
- componentWillUpdate(object nextProps, object nextState)
- componentDidUpdate(object prevProps, object prevState)
- componentWillUnmount()

## this.props.children()
this.props.children的值有三种可能
- 如果当前组件没有子节点，他就是undfined
- 如果有一个子节点，数据类型是object
- 如果有多个子节点，数据类型就是array。
所以处理this.proprs.children的时候要小心。

## PropsType和getDefaultProps
React.PropTypes提供各种验证器（validator）来验证传入数据的有效性。 
使用getDefaultProps方法可以用来设置组件属性的默认值。

# 表单的事件响应和bind复用

## bind复用
bind方法为事件相应函数增加一个参数，事件响应函数通过该参数识别事件源。

*<label>标签里的for不能在正常使用了，而是要写成htmlFor*

## name复用
*为每个标签增加一个name属性值并不友好。*

# 可控组件和不可控组件
## 可控组件
在render()函数中设置了value的<input>是一个功能受限的组件，渲染出来的HTML元素始终保持value属性的值，即使用户输入也不会改变。

这时候你在浏览器中打开的Jspang的值是不可变的，甚至连删除都删除不了，这是由React的渲染策略决定的。如果要写成功能正常和可用性组件，我们需要编写onChange事件，并将value绑定到state中。

*优点*
- 符合React单向数据流特性，即从state流向render输出的结果。
- 数据存储在state中，便于访问和处理。

## 不可控组件

组件完成之后给它加上一个onChange事件，发现是可以监控到变化值的。如果要获得iput中的value值，需先拿到其DOM节点，然后获取其value值。
```js
var  MyForm = React.createClass({
    handleChange:function(){
        var inputValue=ReactDOM.findDOMNode(this.refs.jspang).value;
        console.log(inputValue);
    },
    render:function(){
        return(
            <div>
                <input type="text" onChange={this.handleChange} ref="jspang"/>
            </div>
        )
    }
});
```

