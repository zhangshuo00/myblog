---
title: React笔记（四）-router
date: 2019-10-16 10:45:47
tags:
---
## 路由配置
### 安装
React Router包含三个库，**react-router、react-router-dom、react-router-native**
>npm install --save react-router-dom
### 引入
React Router 通过 Router 和 Route两个组件完成路由功能。
```js
import {BrowserRouter as Router,Route,Link} from 'react-router-dom';
exports default calss Hello extends Component{
    render(){
        return (
            <Router>
                <div>
                    <Route exact path='/' component={Home}/>
                    <Route path='/about' component={About}/>
                </div>
            </Router>
        );
    }
}
```
### BrowserRouter 和 HashRouter
**特点**
- 都是路由的基本组件，需将其放在最外层，选其一使用
- 内部只能含有一个子节点
- BrowserRouter 的URL是指向真实URL的资源路径，页面和浏览器的history保持一致
- HashRouter 使用URL中的hash（#）部分去创建路由
    >http://example.com/#/some/path
- BrowserRouter 创建的URL
    >http://example.com/some/path
### <Route />
- 匹配路径、挂载组件
- ><Route exact path='/home' component={Home}/>
- exact：严格匹配
- path：字符串类型，用来匹配url
- component：值是一个组件，在path匹配成功后挂载这个组件
- render：一个返回组件的方法
- children：一个返回组件的方法






***
## 动态路由
***
## 关于hooks和useEffect
```js

```