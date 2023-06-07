# 一.jsx 语法

1. 传值
class App extends Component {
    render(){
        //每一个组件都只能有一个根元素
        return (
        <>
          <Header />
          <Footer title="hello"/>
        </>
        )
    }
}

2. React内自定义属性和方法
class Footer extends Component {
  render() {
    return <div a={this.props.title}>{this.props.title}我是底部</div>;
  }
}



# 二.style 添加样式

1. 行内标签
<div style={{ color:"red" }}>我是底部</div>;

2. jsx内部使用注释，也要大括号

3. 外层的大括号是jsx的括号，里层的括号是对象的括号

4. key如果是连字符，需要写成小驼峰

5. 如果属性是px，那么px是可以省略的，直接写数字

6. lineHeiht:必须写px单位




# 三.className 添加样式

1. js部分：
import React, { Component } from "react";

<!-- 将写好的css文件引入到组件中-->
import "./footer.css"

class Footer extends Component {
  render() {
    return <div className="aaa">我是底部</div>;
    <!-- class改为：className -->
           
  }
}
export default Footer;

2. css部分
.aaa {
  color: red;
}


# 四.点击字，input框获得焦点

1.htmlFor
 
<label htmlFor="name">姓名：</label>
<input typr="text" id="name"></input>