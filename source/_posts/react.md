title: React 学习笔记
date: 2016-02-24 17:49:14
categories:
tags: [react]
description: 初学react，参考官方文档!
---
[官方文档(中文)](http://www.reactjs.cn)
### 一、教程
1.在 JSX 中，通过使用大括号包住一个 JavaScript 表达式（例如作为属性或者儿子节点），你可以在树结构中生成文本或者 React 组件
2.我们利用 ref 属性给子组件命名，通过 this.refs 引用 DOM 节点。
3.props    从父组件传入的数据会做为子组件的 属性（ property ） ，这些 属性（ properties ） 可以通过 this.props 访问到。（对比props 和 state ）

### 二、react构建应用步骤

1.拆分用户界面为一个组件树（单一功能原则）
2.创建应用的一个静态版本（没有交互功能）（构建应用时，简单应用应使用从上到下的顺序，复杂应用应使用从下到上的顺序）
3.识别出最小的完整的代表UI的state
4.确认 state 的生命周期
5.添加反向数据流(props)

### 三、知识要点整理
1.React 里把事件处理器（event handler）以骆峰命名（camelCased）形式当作组件的 props 传入(富交互性的动态用户界面)
2.如果需要在手机或平板等触摸设备上使用 React，需要调用 React.initializeTouchEvents(true); 启用触摸事件处理。(富交互性的动态用户界面)
3.子级校正:校正就是每次 render 方法调用后 React 更新 DOM 的过程。 一般情况下，子级会根据它们被渲染的顺序来做校正。
4.JavaScript 并不总是保证属性的顺序会被保留数字型属性会按大小排序并且排在其它属性前面。一旦发生这种情况，React 渲染组件的顺序就是混乱。可能在 key 前面加一个字符串前缀来避免
    
    items['result-' + result.id] = <li>{result.text}</li>;
5.spread 语法可以帮助我们把传入组件的 props 复制到对应的 HTML 元素上

    var CheckLink = React.createClass({
      render: function() {
        // 这样会把 CheckList 所有的 props 复制到 <a>
        return <a {...this.props}>{'√ '}{this.props.children}</a>;
      }
    });
6.React.PropTypes.element 可以限定只能有一个子级传入。
    
    var MyComponent = React.createClass({
      propTypes: {
        children: React.PropTypes.element.isRequired
      },
    
      render: function() {
        return (
          <div>
            {this.props.children} // 有且仅有一个元素，否则会抛异常。
          </div>
        );
      }
    
    });
7.注意：从 render() 中返回的内容并不是实际渲染出来的子组件实例。从 render() 返回的仅仅是子组件层级树实例在特定时间的一个描述。
8.注意， this.props.children 的值有三种可能：如果当前组件没有子节点，它就是 undefined ;如果有一个子节点，数据类型是 object ；如果有多个子节点，数据类型就是 array 。所以，处理 this.props.children 的时候要小心。
    





