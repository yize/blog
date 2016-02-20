---
layout: post
title: "Study React"
date: 2015-09-21 00:00:00
tags:
 - study
 - react
---

# React 学习笔记

> A JAVASCRIPT LIBRARY FOR BUILDING USER INTERFACES

引言是 [React 官网](http://facebook.github.io/react/) 上是的自述。React 主要是用于构建用户界面。

## 为什么使用 React?

React 是一个 Facebook 和 Instagram 用来创建用户界面的 JavaScript 库。主要采用以下两个思想：

- 简单

	仅仅只要表达出你的应用程序在任一个时间点应该长的样子，然后当底层的数据变了，React 会自动处理所有用户界面的更新。

- 声明式

	 数据变化后，React 概念上与点击“刷新”按钮类似，但仅会更新变化的部分。

<!--more-->

## 几个特点

- 仅仅是 UI

	许多人使用 React 作为 MVC 架构的 V 层。尽管 React 并没有假设过你的其他技术栈，但你仍可以作为一个小特征轻易地在已有项目中使用。

- 虚拟 DOM

	React为了更高超的性能而使用虚拟DOM作为其不同的实现。 它同时也可以由服务端Node.js渲染 － 而不需要过重的浏览器DOM支持。

- 数据流

	React实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。
	

## 几个概念

-  React elements

	`React 元素（React elements）` 是一些用于表示 HTML 元素的 JavaScript 对象，他们并不存在于浏览器中，浏览器原生对象在 React 中，也有对应的 React 元素对应，比如 `h1` 、 `div` 、`section`。


- Components

	`组件（Components）`也就是我们常说的组件，他们一般是构成我们页面的最大的一部分，主要包括「结构」和「功能」。举个例子，比如 `NavBar` 、 `LikeButton` 、`ImageUploader` 都是一个个带有结构和功能的组件。

	组件就像是函数。接受`props`和`state`作为参数，渲染出`HTML`。

- JSX

	`JSX` 是一个看起来像 XML 的 JavaScript 语法扩展。举个例子：`<h1>Hello</h1>` 是 `React Element` 使用 `JSX` 的语法的写法。同样的，如果你不用 `JSX` ，使用这样的写法：`React.DOM.h1(null, 'Hello')` 也可以达到相同的效果。相比之下 `JSX` 的易读性更好。 JSX 需要编译之后才能在浏览器中运行。`JSX` 并不是强制使用的，这个语法只是让搭建 React 应用变得更加地简单。
	
	所有的标签都必须闭合，可以是自闭合也可以是常规闭合。`<div/>` 和 `<div></div>` 是等价的。
	


- The Virtual DOM

	`虚拟 DOM（The Virtual DOM）`  是存在于内存之中的一种数据结构，并不是真正的 DOM 节点。只有当他插入到文档中以后，才会变成真正的 DOM 。React 会监听虚拟 DOM 的变化，会自动的计算 DOM 和 虚拟 DOM 的区别。所有 DOM 的变动，都会先在 虚拟 DOM 上发生，然后再将实际变动的部分，反应在真实的 DOM 上，这种算法叫 DOM diff ，它极大的提高了网页性能表现。

需要先稍微理解下以上的几个概念，方便接下来的理解。

## 渲染

我们首先来看下怎么把 虚拟 DOM （React 元素和组件都是虚拟 DOM）渲染到页面上。虚拟 DOM 只存在于内存中，我们需要告诉 React 生成的 DOM 应该渲染到何处。

``` javascript
React.render(<h1>Hello World</h1>, document.getElementById('App'));
```

[View JSBin](http://jsbin.com/herina/edit?html,js,output)

上面的代码会将一个 H1 ，插入到 body 上。

`render` 函数接收两个参数，第一个参数为 `React element`，第二个参数为 `DOM element`。

## 组件

组件是 React 的重要组成部分，是自定义的 React 元素。一个组件就是一个功能模块。

``` javascript
var Hello = React.createClass({
	render: function(){
		return (<h1>Hello</h1>)
	}
})

React.render(<Hello/>, document.getElementById('App'));
```

[View JSBin](http://jsbin.com/hitalak/edit?html,js,output)

通过 React.createClass 方法创建组件类，每个组件类方法必须提供 `render` 函数。`render` 函数返回虚拟 DOM 结构树标示串。

在上段代码中，通过 `createClass` 我们创建了 `HelloWorld` 元素，然后我们通过 `React.render` 方法告诉 React 需要将 `HelloWorld` 元素渲染到 `#app` 里面。

这个例子和上一个差不多，区别是你可以为 `HelloWorld` 元素添加更多的自定义方法和逻辑了。

> 注意 自定义的 React 元素，第一个字母需要大写，用来和传统的 HTML 元素进行区分。


##  Props

`Props` 我们可以理解为组件的参数。通过 `HTML` 的属性传入。

``` javascript
var Hello = React.createClass({
	render: function(){
		return (<h1>Hello {this.props.name}</h1>)
	}
})

React.render(<Hello name='World'/>, document.getElementById('App'));
```

[View JSBin](http://jsbin.com/rudipo/edit?html,js,output)

在 `React.render` 方法中，我们传入了 `name` 这个参数。这个参数在 `Hello` 组件的 `render` 通过 `this.props.name` 取得。

所有通过 `ReactElement` 传入的参数，都可以在组件的 `render` 方法中获取到。值得注意的是，`ReactElement` 是通过 `JavaScript` 创建的，`class` `for` 等均为 `JavaScript` 的保留字，在 `JSX` 中不能直接写 `class` 和 `for`，而需要写成 `className` 和 `htmlFor`：

``` javascript
React.render(<label htmlFor="inputEl"><input type="text" className="input-el" id="inputEl"/></label>,document.getElementById("App"))
```

### 行内样式的写法

行内样式的写法，跟 HTML 的区别比较大，以对象的形式传入。

``` javascript
var Hello = React.createClass({
	render: function(){
		return (<h1 style={{color:'red'}}>Hello {this.props.name}</h1>)
	}
})

React.render(<Hello name='World'/>, document.getElementById('App'));
```

[View JSBIN](http://jsbin.com/riyayo/edit?html,js,output)

style 不能写成 

``` javascript
style="color:red"
```

而应该写成

``` javascript
style={{color:'red'}}
```



### this.props.children

this.props 对象的属性和组件的属性一一对应，但是有一个是例外的， 就是 `this.props.children` 。它表示的是组件的所有子节点。

``` javascript
var List = React.createClass({
  render: function() {
    return (
      <ul>
      {
        this.props.children.map(function (child) {
          return (<li>{child}</li>)
        })
      }
      </ul>
    );
  }
});

React.render(<List><span>Hello</span><span>World</span></List>,document.getElementById('App'))
```

[View JSBin](http://jsbin.com/xeliho/edit?html,js,output)

> 注意：你没有办法通过 `this.props.children` 取得当前组件的子元素，因为 `this.props.children` 返回的是组件传递给你的 `Passed onto you` 子节点。

值得一提是，`this.props.children` 的返回类型，跟子元素的个数有关。

```
0 undefined
1 React Element
2+ Array of React Element
```

如果你确定长度大于等于2，你可以直接通过 this.props.children.map 方法，否则就会报错。

React 提供了 React.Children ，用来帮我们处理这样的 case 。

上面的代码可以直接把  

``` javascript
{
   this.props.children.map(function (child) {
     return (<li>{child}</li>)
   })
 }
```

替换为：

``` javascript
{
   React.Children.map(this.props.children, function (child) {
     return (<li>{child}</li>)
   })
 }
```

这样的话，就不会有问题了。

具体的可以去看下 [React.Children - React 官方文档](https://facebook.github.io/react/docs/top-level-api.html#react.children)

## State


State 是组件的内部状态对象，state 仅用于实现交互功能，数据会随着时间变化。

``` javascript
var SayHello = React.createClass({
	getInitialState: function(){
		return {
			value: "World"
		}
	},
	handleChange: function(){
		this.setState({
			value:e.target.value
		})
	},
	render: function(){
		return (
			<div>
				<h1>Hello {this.state.value}</h1>
				<input type="text" value={this.state.value} onChange={this.handleChange}/>
			</div>
		)
	}
})

React.render(<SayHello/>, document.getElementById('App'))
```

[View JSBin](http://jsbin.com/xefore/edit?html,js,output)

> Components are Just State Machines

React 认为组件仅仅是状态机这么简单，在 React 中，你只需要管理组件的状态[state]来更新 UI 的展现，然后根据新的状态来渲染出新的 UI。根据新的状态更新 DOM 这件事情，React 替我们做了，而且做的很好。我们只需要享受编码的乐趣就行了。

`setState(data, callback)` 是 React 用来设置状态的方法，第一个参数是个对象，里面需要传入你想要更改的键值对；第二个参数是可选的，组件重新渲染之后会触发这个函数，这个参数大部分时候是用不上的，React 会帮你处理 setState 之后的逻辑。

`getInitialState` 在组件初始化到时候，会调用这个方法，用以获取默认的 State 值，这个函数返回一个对象。

`handleChange` 是我们自己实现的方法，用来触发 `setState` 方法，`onChange={this.handleChange}` 我们在 input 的 onChange 时，触发了 `handleChange` 方法，在 handleChange 中调用 setState 方法改变了 this.state.value 的值，这个时候会触发 render 方法。注意：调用 setState 方法都会触发 render 方法，生成虚拟 DOM ，然后 React 会进行 DC（Dirty Check），从而决定是否要将虚拟 DOM 反映到页面上。


## Props vs. State

这两者是有关系的，一个组件的 state 可能会成为另外一个组件的 props 。 state 通过 render 方法传给另外一个组件。

``` javascript
<ChildComponent value={this.state.value}/>
```

我们暂且称这个组件为子组件，它的父级组件为父组件。父组件的 state.value 变成了子组件的 `this.props.value` ，对于子组件来说，props.value 是不允许被更改的。如果需要更改，需要父组件通过改变其自身的 state 来改变：

``` javascript
this.setState({value:'New Value'});
```

React 会将值传递给子组件。这个时候，我们可能会问：如果子元素想要改变自己的这个 prop ？一般情况下，都是通过父组件监听子组件的事件来完成：

``` javascript
<ChildComponent value={this.state.value} onChange={this.handleValueChange}/>
```

父组件中的 handleValueChange 方法大概是这样的：

```javascript
handleValueChange: function(newValue){
	this.setState({ value: newValue});
}
```

大部分组件自身都不需要有 state ，除非内部需要维护组件自身的状态。


## 表单

入门 React 时，难以习惯的是 input、textarea 等元素的输入了，用户在填写表单的值的时候，属于用户跟组件的互动。input 的值变化需要在 onChange 等事件抛出，通过 value 传递给 input ，从而改变输入值，React 会自动渲染组件，并且把光标定位到它应该在的位置。

如果仅仅是如下这样的代码，效果跟我们想象的可能不太一样，不管我们怎么输入，就是不会有效果。

``` html
<input type="text" value="hello"/>
```

[View JSBin](http://jsbin.com/durogu/edit?html,js,output)

细心的你可能会发现，如果你把光标移动到除了 o 之外的位置，输入以后，会回到 o 的后面。但是值不会发生改变。

对 React 来说，如果我们赋予了表单元素（input、textarea、option等） value 值，却没有 onChange 方法去处理事件，React 会把这个表单元素渲染为只读元素，如果需要编辑功能，你应该用 defaultValue 替代。 要么设置 onChange 要么推荐直接写 readonly 好了。更多 Form 组件和原生组件的区别可以看[这里](https://facebook.github.io/react/docs/forms.html)



``` html
<!--1. onChange-->
<input type="text" value="hello" onChange={this.handleChange}/>
<!--2. defaultValue-->
<input type="text" defalutValue="hello"/>
<!--3. readOnly-->
<input type="text" value="hello" readOnly/>
```


- value ， `<input>`、`<textarea>` 支持
- checked， `<input>` type 为 `checkbox` 和 `radio` 的支持
- selected， `<option>` 支持

在 HTML 中，textarea 是通过他的 children 赋值的，但是在 React 中则是通过 value。

Form 组件允许通过 `onChange` 回调来监听值的变化， onChange 会在以下几种情况下都会触发：

- `<input>`、`<textarea>` 的 value 发生改变
- `<input>` 的 checked 值发生改变
- `<option>` 的 selected 值发生改变

和所有 DOM 事件一样，所有的 HTML 原生组件都支持 onChange 属性，而且可以用来监听冒泡的 change 事件。React 也提供了捕获事件，在冒泡事件名后加上 `Capture` 就可以监听捕获事件。

``` javascript
onChange 监听冒泡阶段的 change 事件
onChangeCapture 监听捕获阶段的 change 事件
```

## 事件

React 和 jQuery 一样，标准化了事件，也封装了事件对象，使得在浏览器中不存在兼容性问题。如果你想要直接使用底层的浏览器事件对象，也可以直接通过 `nativeEvent` 访问。

参考：[React events - supported-events](http://facebook.github.io/react/docs/events.html#supported-events)

## FindDOMNode()

React Element 都不是真实的 DOM 对象，而是虚拟 DOM（Virtual DOM）。React 提供了 `React.findDOMNode` 的方法来取到组件的真实 DOM。

``` js
var SayHello = React.createClass({
	getInitialState: function(){
		return {
			value: "World"
		}
	},
	componentDidMount: function(){
		var headRef = this.refs.head;
		var headEl = React.findDOMNode(headRef);// 等价于 headRef.getDOMNode()
		headEl.style.color = 'red';
	},
	handleChange: function(){
		this.setState({
			value:e.target.value
		})
	},
	render: function(){
		return (
			<div>
				<h1 ref="head">Hello {this.state.value}</h1>
				<input type="text" value={this.state.value} onChange={this.handleChange}/>
			</div>
		)
	}
})

React.render(<SayHello/>, document.getElementById('App'))
```

[View JSBIN](http://jsbin.com/sivivi/edit?html,js,output)

> 注意，我们必须在组件挂载到页面之后才能获取到它对应的真实 DOM 元素，我们不能在组件 Mount 之前获取到 DOM 元素。

## 组件的生命周期

我们可以从几个方面来理解 React 组件的生命周期。

1. 初始化，也就是挂载（Mount）时，发生了什么？
2. 更新， 组件挂载之后，props 或者 state 更新时，发生了什么？
3. 移除，组件从 DOM 中移除时，发生了什么？

### 初始化


![React-initial](https://img.alicdn.com/tps/TB1Jme3JVXXXXXcXpXXXXXXXXXX-1032-408.png)

在组件初始化时，会调用一次 `getDefaultProps` 和 `getInitialState` 。

`getDefaultProps` 方法用来设置默认 props

`getInitialState` 方法用来设置 state 的初始值
 
在 `render` 之前，会触发 `componentWillMount`

注意下，在这个方法中调用 setState 不会触发组件的第二次渲染。

在 `render` 之后，会触发 `componentDidMount`

此时，我们已经可以取到真实的 DOM 节点，可以进行 DOM 操作了。

我们也可以在此时做数据请求。比如 ajax

`render` 方法会返回组件需要的标记，React 会根据标记生成虚拟 DOM。

### 改变 props

props 发生改变时，会触发这几个方法：

![React-changeProps](https://img.alicdn.com/tps/TB1KpKQJVXXXXbcXFXXXXXXXXXX-1020-392.png)


`componentWillReceiveProps` 方法会在组件接收到新的 props 的时候调用。

用这个函数可以在 React 接收 props 之后，render 渲染之前更新 state 。在这个函数中，可以调用 this.setState 方法来改变 state ，而不会引起第二次渲染。

`shouldComponentUpdate` 方法会在 `render` 方法之前执行，用来告诉 React 是否需要重新渲染当前组件。这个方法返回的是 Boolean 值。这个方法不会在组件初始化的时候执行。


`componentWillUpdate` 方法会在 `shouldComponentUpdate` 返回 true 之后立即执行。我们不能在这个方法中使用 `this.setState` 如果需要更新 state 来响应某个 prop 改变，需要使用 `componentWillReceiveProps`

`componentDidUpdate` 方法会在组件的更新已经同步到 DOM 中之后，以及被调用。

这些方法都不会在组件初始化的时候调用。

### 改变 State

state 发生改变，会触发这几个方法：

![React-updateState](https://img.alicdn.com/tps/TB17cW0JVXXXXagXpXXXXXXXXXX-1012-336.png)


这些方法都不会在组件初始化的时候调用。


### 移除

![React-unMounting](https://img.alicdn.com/tps/TB1ityWJVXXXXbCXpXXXXXXXXXX-1006-152.png)

组件移除之前，会触发 `componentWillUnmount`方法，我们可以使用该方法来执行必要的清理，比如去除无效的定时器，移除在 componentDidMount 时创建的 DOM 元素等。


## 参考链接

- [React 官网](http://facebook.github.io/react/)
- [React 入门实例教程](http://www.ruanyifeng.com/blog/2015/03/react.html)
- [React Component Lifecycle](http://busypeoples.github.io/post/react-component-lifecycle/)
- [Reactjs.cn](http://reactjs.cn/react/index.html)
- [DOM diff](http://calendar.perfplanet.com/2013/diff/)












