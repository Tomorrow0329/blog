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