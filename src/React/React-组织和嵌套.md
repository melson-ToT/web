
# 五.函数式组件

import React from 'react';
import ReactDOM from 'react-dom/client';

<!-- 在 React 内，首字母大写的是组件，小写的元素 -->
const App = (props) =>{
  return <div>{props.name}你好!</div>
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App name="张非-"/>)



# 六. class 类组件

import React from 'react';
import ReactDOM from 'react-dom/client';

class App extends React.Component {
  render(){
    console.log(this);
    <!-- this 指向的是 App-->

    return <div>{this.props.name}你好！</div>
<!--这里必须要用 this.props-->
  }
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App name="张非-"/>)



# 七.组件的组合和嵌套

1. src文件的 index.js 文件，是项目的入口文件

2. 在src文件夹中，建立一个home的文件，在home内建立相应的组件，

3. 再将建立的组件挂载到，src的 index.js 入口文件中

4. src的 index.js 入口文件：
<script>
import React from 'react';
import ReactDOM from 'react-dom/client';

import App from "./home/App"
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />)

5. hone与index.js 入口文件，平齐(相当于vue中的 main.js)

6.  hone下的App.js 组件
import React from "react"
class Header extends React.Component {
    render(){
        return <header>我是头部组件</header>
    }
}
const Footer = () =>{
   return  <footer>我是底部组件</footer>
}
class App extends React.Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <div>
          <Header />
          <Footer />
        </div>
        )
    }
}
export default App



# 八.组件的占位符

1. 一般组件内的嵌套嵌套多个组件，所以，要用一个元素把他们包起来，且多个组件 return要加()，return()
class App extends React.Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        //由于每一个组件都只能有一个根元素
        <div>
          <Header />
          <Footer />
        </div>
        )
    }
}

2. 如果想要将这个 <div>编程占位符，要用：<React.Fragment>标签
class App extends React.Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <React.Fragment>
          <Header />
          <Footer />
        </React.Fragment>
        )
    }
}

3. <React.Fragment>的简化写法--{Fragment}
import React ,{Fragment}from "react"

class Header extends React.Component {
    render(){
        return <header>我是头部组件</header>
    }
}
const Footer = () =>{
   return  <footer>我是底部组件</footer>
}
class App extends React.Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <Fragment>
          <Header />
          <Footer />
        </Fragment>
        )
    }
}
export default App

4. <React.Fragment>的简化写法--<></>
import React from "react"

class Header extends React.Component {
    render(){
        return <header>我是头部组件</header>
    }
}

const Footer = () =>{
   return  <footer>我是底部组件</footer>
}

class App extends React.Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <>
          <Header />
          <Footer />
        </>
        )
    }
}

export default App

5. React.Component--的简化写法：

将 Component 在 React 中，解构
import React ,{Component}from "react"

class Header extends Component {
    render(){
        return <header>我是头部组件</header>
    }
}
const Footer = () =>{
   return  <footer>我是底部组件</footer>
}
class App extends Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <>
          <Header />
          <Footer />
        </>
        )
    }
}
export default App

6. 从 React 解构的东西，首字母大写的是组件：
如：import React ，{Fragment，Component}from "react"

7. 从 React 解构的东西，首字母小写的是方法：





# 九.真正的 React 项目，跟vue一样，一个组件对应一个js

1. 父组件
import React ,{Component}from "react"
import Header from './Header'
import Footer from './Footer'

class App extends Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <>
          <Header />
          <Footer />
        </>
        )
    }
}
export default App

2. 子组件
import React ,{Component}from "react"

class Header extends Component {
    render(){
        return (
            <div>我是头部</div>
        )
    }
}

export default Header

3. 子组件
import React, { Component } from "react";

class Footer extends Component {
  render() {
    return <div>我是底部</div>;
  }
}

export default Footer;
