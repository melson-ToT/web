# 一.React 脚手架

第一步，全局安装：npm i -g create-react-app

第二步，切换到想创项目的目录，使用命令：create-react-app hello-react

第三步，进入项目文件夹：cd hello-react

第四步，启动项目：npm start

第五步，Vscode 插件安装 ES7 React/Redux/GraphQL/React-Native snippets 代码模板插件，就可以输入rcc 直接填入类似组件模板代码。
————————————————
版权声明：本文为CSDN博主「fang·up·ad」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_22310551/article/details/120879850


# 二.yarn 安装

全局安装：npm install -g yarn

查看版本：yarn --version

淘宝镜像安装：

yarn config set registry https://registry.npm.taobao.org -g

yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g

//常见的yarn命令：

yarn start 运行项目
yarn build 打包
yarn eject react ：把webpack的配置文件都隐藏起来了，这个命令是将所有webpack相关的配置文件都暴露出来，并且这个命令是不可逆转的，不能再隐藏webpack的配置文件。
 安装React脚手架步骤
打开cmd输入：npm i -g create-react-app //全局安装
切换到想要创建项目的目录，cmd后输入：create-react-app hello-react // hello-react是你自定义的项目名称
安装成功后cd到项目文件夹
启动项目：yarn start 或者 npm start
————————————————
版权声明：本文为CSDN博主「Embrace_L」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/xixi8361/article/details/128187113



# 三.删除src 中自带的文件

1. 只留 index.js 文件

2. index.js 文件 中：

import React from 'react';
<!-- 引入React，react的核心代码 -->
import ReactDOM from 'react-dom/client';
<!-- 引入ReactDOM，用于开发浏览器网页 -->

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <div>你好</div>
)


# 四.删除 public文件夹中自带的文件

只留：favicon.ico 和 index.html



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





由于每一个组件都只能有一个根元素，所以