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
    **http://example.com/#/some/path**
- BrowserRouter 创建的URL
  **http://example.com/some/path**
- Router 会创建一个history对象，history用来跟踪URL，当URL发生变化时，Router的后代组件会重新渲染。ReactRouter 中提供的其他组件可以通过 context获取 history对象，ReactRouter 中其他组件必须作为Router组件的后代使用，但只能包含唯一一个子元素。
```js
ReactDOM.render(
    return(
        <BrowserRouter>
            <App />
            //<App />
        </BrowserRouter>
    ),document.getElementById('root')
)
```
### <Route /> 路由器
**每当有一个组件需要根据URL决定是否渲染时，就需要创建一个Route**
- 匹配路径、挂载组件

```js
<Route exact path='/home' component={Home}/>
```

**1. path**
    **当使用 BrowserRouter 时，path 用来描述这个Route 匹配的URL的pathname；当使用HashRouter 时，path 用来描述这个Route 匹配到的URL的 hash。当URL 匹配一个Route时，这个 Route中定义的组件就会被渲染出来。**

**2. match**
    **当URL和Route匹配时，Route 会创建一个 match 对象作为props 中的一个属性传递给被渲染的组件，以下为对象包含的属性：**
（1）params：Route的path 可以包含参数，例如<Route path="/foo/:id"/>。params就是用于从匹配的URL中解析出 path 中的参数。例如，当 URL = 'http://example.ocm/foo/1' 时，params= {id: 1}。
（2）isExact：布尔值，判断URL 是否完全匹配。例如，当 path='/foo'、URL="http://example.com/foo" 时，是完全匹配; 当 URL="http://example.com/foo/1" 时，是部分匹配。
（3）path：Route 的path 属性，构建嵌套路由时会使用到。
（4）url：URL 的匹配的方式

**3. Route 渲染组件的方式**
   （1）component
   component 的值是一个组件，当URL 和Route 匹配时，component属性定义的组件就会被渲染。
   ```js
   <Route path='/foo' component={foo}/>
   //当URL = 'http://example.com/foo'时，Foo 组件会被渲染
   ```
   （2）render
   render 的值是一个函数，返回一个React 元素，并且可以为待渲染的组件传递额外的属性。
   ```js
   <Route path='/foo' render={(props)=>{
       <Foo {...props} data={extraProps}/>
       //Foo 组件接收一个额外的data 属性
   }}/>
   ```
   （3）children
   children 的值是一个函数，返回要渲染的React 元素，但无论是否匹配成功，返回的组件都会被渲染。

**4. Switch 和exact**
    当URL 和多个Route 匹配时，这些Route 都会被渲染，但如果只想让第一个匹配的Route 沉浸，可以把这些Route 放到一个Switch 组件中。如果想让URL 和Route 完全匹配时才渲染，可以使用Route 的exact 属性。
    ```js
    <Router>
        <Switch>
            <Route exact path='/' component={Home}/>
            <Route exact path='/posts' component={Posts} />
            <Route exact path='/:user' component={User} />
        </Switch>
    </Router>
    ```
**5. 嵌套路由是指在Route 渲染的组件内部再定义新的Route。**
### 链接
**Link 是React Router提供的链接组件，当点击时，页面该跳转到哪个路由**
```js
<header>
    <ul>
        <li><Link to='/'>Home</Link></li>
        <li><Link to='/post'>Post</Link></li>
    </ul>
</header>
```
使用to 属性声明要导航到的URL 地址，当to 为object 类型时，可以包含pathname、search、hash、state四个属性。
```js
<Link to={{
  pathname: '/posts',
  search: '?sort=name',
  hash:'#the-hash',
  state: { fromHome: true}
}}>
</Link>
```
除了使用Link ，还可以使用history 对象手动实现导航。history 中的两个方法:push(path,[state])会向浏览器新增一条记录 和 replace(path,[state])会用新纪录替换记录。
```js
history.push('/posts');
history.replace('/posts');
```
***
## 动态路由
***
## 关于hooks和useEffect