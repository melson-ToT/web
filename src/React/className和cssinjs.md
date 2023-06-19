
# 一.在不同的条件加不同的样式

1. 在 React 里面，使用 state 的对象来作为响应式数据

2. className 以变量的形式，简单类型的判断，用三目

import React, { Component } from "react";
import "./zhangfei.css"
class Zhangfei extends Component {
  state = {
    done:false
  }
  render() {
    return (
      <>
        <h2>使用className给不同的条件添加不同的样式</h2>
        <p className={this.state.done ? "wanchen" :"unwanchen"}>你好-张非</p>
      </>
    );
  }
}
export default Zhangfei;

.wanchen {
    color: green;
}
.unwanchen {
    color: red;
}




# 二. className 以变量的形式，复杂类型的判断，用 classnames 的包

1. 搜索 -> npmjs.com -> 将 classnames 粘贴带搜索框 -> 

2. 安装：npm i classnames

3. 在组件中引入：classnames
import classNames from 'classnames/bind';

4. 在组件中引入标签的的 css
import zhangfei from './zhangfei.css';
  <!--这个zhangfei 随便取名字 -->

5. 执行 bind 方法，拿到一个 cx 函数，cx这个变量随便取



# 三.用 classnames 的包，做复杂类型的判断

1. 案例1
<script>
import React, { Component } from "react";
import classNames from 'classnames/bind';//在组件中引入：classnames
import zhangfei from './zhangfei.css';//在组件中引入：对应标签的css

let cx = classNames.bind(zhangfei);//将这个css 赋值给cx

class Zhangfei extends Component {
  state = {
    done:false//先将done为：false
  }
  render() {
    let className = cx({
      wanchen:this.state.done,
      unwanchen:!this.state.done,//取反
    })
    return (
      <>
        <h2>使用className给不同的条件添加不同的样式</h2>
        <p className={className}>你好-张非</p>
      </>
    );
  }
}
export default Zhangfei;

2. 案例2

<script>
import React, { Component } from "react";
import classNames from 'classnames/bind';
import zhangfei from './zhangfei.css';
let cx = classNames.bind(zhangfei);

class Zhangfei extends Component {
  state = {
    done:false//先将done为：false
    num:3//在支付后台页面，可能用
  }
  render() {
    let className = cx({
      const {done,num} = this.state
      wanchen:done && num === 3,当支付成功时，后台用户页面字体颜色改变
      unwanchen:!done,//取反
    })
    return (
      <>
        <h2>使用className给不同的条件添加不同的样式</h2>
        <p className={className}>你好-张非</p>
      </>
    );
  }
}
export default Zhangfei;




# 四.css-in-js

1. 搜索 -> npmjs.com -> 将 styled-components 粘贴带搜索框 -> 

2. 安装：npm i styled-components
    或：yarn add styled-components

3. 就可以在js内，写css

import React, { Component } from "react";
import styled from "styled-components"--引入styled-components包

const Hello = styled.p` //Hello代替了p标签，但是Hello具有p标签的标签属性
  color:red;
  font-size:30px;
`

class Zhangfan extends Component {
  render() {
    return (
      <>
        <h2>使用css-in-js</h2>
        <Hello>你好-张凡</Hello>----这里的 Hello代替了p标签
      </>
    );
  }
}
export default Zhangfan;





