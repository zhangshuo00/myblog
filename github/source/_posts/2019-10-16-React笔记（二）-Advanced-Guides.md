---
title: React笔记（二）-Advanced Guides
date: 2019-10-16 08:37:03
tags:
---
# Context
>Context 提供了一种在组件之间共享此类值的方式，而不必显示地通过组件树的逐层传递 props
![context.png](https://i.loli.net/2019/10/17/17UKldQYfwgcJZt.png)

就是把`context`当作一个组件树内共享的store，用以传递数据。基于树形结构共享的数据：**在某个节点开启提供context后，所有后代节点component都可以获得共享的数据**

## 使用Context
Context的使用基于`生产者消费者模式`，即生产者（Provider）通常是一个父节点，消费者（Consumer）通常是一个或多个子节点。
`App.js`
```js
import React from 'react';
import ReactDOM from 'react-dom';
export const con = React.createContext()//通过静态方法React.createContext()创建Context对象，对象包含两个组件<Provider /> <Consumer />

export default class App extends Component {
    render(){
        return (
            //使用一个Provider 将当前的值（dark）传递下去
            <Con.Provider value='dark'>
                <Toolbar />
            </Con.Provider>
        );
    }
}
function Toolbar (props){
    return (
        <Button/>
    )
}
```
后代组件根据需要，指定`contextType`需要作用的组件树范围
`Child.js`
```js
import React,{Component} from 'react';
import {con} from './App'

export default class Child extends Component{
    //指定contextType读取当前的 value
    //react 会找到最近的value context 然后使用
    static contextType = Con;
    render(){
        return (<Button theme={this.context}/>);

        //也可以使用<Consumer>组件指定消费者
        // return (
        //     <Con.Consumer>
        //         (value)=><Button theme={value}>
        //     </Con.Consumer>
        // )
    }
}
//除了写static contextType = Con; 也可以这样写
Child.contextType = con;
```

***
# HOC
>HOC 就是一个函数，且该函数接收一个组件作为参数，并返回一个新组件
```js
import React,{Component} from 'react'

export default class Hoc extends Component{
    render(){
        return (
            <div>
                <MyMusic />
                <MyMusic1 />
            </div>
        )
    }
}
//实例化对象
var MyMusic = hoc(Music,url,'one');
function hoc(Com,url,title){
    class A extends Component{
        constructor(){
            super();
            this.state={
                data:[]
            }
        }
        componentDidMount(){
            Axios.get(url)
            .then((res)=>{
                this.setState({
                    data:res.data.result
                })
                console.log(res);
            })
        }
        render(){
            return(
                <div>
                    <h1>{title}</h1>
                    <Com data={this.state.data}>
                </div>
            )
        }
    }
}
```
***
# Portals
>Portals提供了一种能让子节点渲染到父组件之外的方式
```js
ReactDOM.createPortal(child,container);
//child 是任何可渲染的React子元素
//container 是一个DOM元素
```
当父组件有`overflow:hidden / z-index`时，需要子组件能够在视觉上跳出容器时使用。

