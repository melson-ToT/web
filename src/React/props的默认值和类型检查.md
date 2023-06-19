# 一.props 类组件的默认值

1. props的默认值,是不可改变的


2. 但是可以通过 static defaultProps 来改变

import React, { Component } from "react";
class YiJun extends Component{
  <!-- //类组件的 props 的默认值的写法，父组件没有 num，自身可以在 props 内，定义一个值，通过 props 进行传值 -->
  <!-- //static defaultProps 是固定写法，不能更改 -->
  <!-- //static  表示类的私有属性 -->
  static defaultProps = {
    num:20,
  }
  render(){
    return (
      <p>{this.props.num}</p>
    )
  }
}

export default YiJun;


3. 也可以通过在：类的原型上挂载属性
import React, { Component } from "react";

class YiJun extends Component{
  render(){
    return (
      <p>{this.props.num}</p>
    )
  }
}

<!-- 类的私有属性 = 在类的原型上挂载属性 -->
YiJun.defaultProps = {
  num:50
}

export default YiJun;



# 二.props 函数组件的默认值

1. props的默认值,是不可改变的


2. 函数组件不可以通过 static defaultProps 来改变，因为函数组件没有 static defaultProps，但是可以通过 原型上挂载属性


3. 也可以通过：原型上挂载属性

const YiJun = (props) =>{
  return (
    <p>{props.num}</p>
  )
}

<!-- 函数组件的属性 = 在函数组件的原型上挂载属性 -->
YiJun.defaultProps = {
  num:60
}

export default YiJun;