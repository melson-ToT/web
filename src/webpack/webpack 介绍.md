# 一.打包

1. npm run build ----打包，压缩代码

2. 讲写好的代码发送到测试环境



# 二.webpack 安装

1. 全局安装

cnpm i webpack webpack-cli -g
yarn add webpack webpack-cli -g

2. 局部安装
cnpm i webpack webpack-cli -D
yarn add webpack webpack-cli -D


# 三.将 webpack 局部安装完毕之后，建立一个webpack-demo,直接在webpack-demo内写代码

1. 建立一个src文件夹，在src中建立 index.js 的文件

2. index.js 的文件，就是入口文件

3. 直接在命令行:webpack

4. 会自动生成一个dist的文件夹，内部的 main.js 文件，就会把 src 的 index.js 的文件，进行打包

5. 直接在命令行:webpack --mode development/production 开发环境/生产环境

webpack --mode development/production 开发环境/生产环境



# 四. webpack.config.js -- 这个文件就是用来做 webpack 的配置文件

1. 建立一个 webpack.config.js文件

2. 配置文件是一个 node.js文件

3. 案例：
const path = require('path')

module.exports = {
    entry:（'./src/index.js'）,
    output:{
        path:path.resolve(_dirname,'dist'),
        filename:'bundle.js'
    }
}



# 五. webpack 的核心模块

1. 模式：开发环境/生产环境

module.exports = {
    <!-- mode指定了打包的模式为：生产环境 -->
    mode:"production"
}

2. 入口：指定那个文件是我们的入口文件
module.exports = {
    <!-- entry是用来配置指定那个文件，是我们的入口文件 -->
    entry:'./src/index.js',
}

3. 出口：output是用于配置出口的

    output:{
        path:path.resolve(_dirname,'dist'),
        <!-- 将文件打包到 dist文件中，而这个dist文件，在局部配置中，已经自动生成了-->
        filename:'index.js'// main.js
        <!-- filename：将dist文件内的 main.js换成 index.js文件，设置成  main.js也可以->
    }

4. loader转换器:就是将我们的 css 和 html 文件转为js文件

(1)案例：
     直接将全局的css文件引入 index.js入口文件，直接报错

*{
    margin: 0;
    padding: 0;
}
html,body {
    width: 100%;
    height: 100%;
}

在 index.js入口文件 引入全局的css文件，直接报错
import style.css from "./style.css"


(2)案例：module 就是 loader转换器
<!-- loader的作用就是将其他类型得到文件转成 webpack 认识的js文件-->
module:{
    <!-- rules（规则）：是一个数组，数组里面的每一个对面就是转换器 -->
    rules:[
        test: /\.css$/,
        use: ["css-loader"],
    ]
}


(3)案例：
      搜索：webpackjs.com/loaders/css-loader
      可以将图片、url等进行转换


(4)案例：
      安装：cnpm i --save-dev css-loader
module:{
    rules:[
        <!-- 转换器安装后，是不需要引入的 -->
        test: /\.css$/,
        use: ["style-loader","css-loader"],
        <!-- 我们先将css转为js，再将js，转为css，所以，先转换的，要写在后面："css-loader" -->
    ]
}


5. 插件：loader转换器做不了的事情，交给插件做

1.点击右侧：Plugin

2.安装：npm install --save-dev html-webpack-plugin

3.插件是需要引入到文件中，转换器则不需引入

4.引入：
const HtmlWebpackPlugin = require('html-webpack-plugin');

<!-- plugin 表示数组，每一项代表一个插件 -->
5.plugins: [new HtmlWebpackPlugin()],



# 六. webpack 的核心模块的案例

安装：cnpm i --save-dev css-loader    
<!-- 将css转为js -->

npm install --save-dev html-webpack-plugin
<!-- 在打包文件中自动生成一个HTML文件 -->

const HtmlWebpackPlugin = require('html-webpack-plugin');
<!-- 引入插件 -->

const path = require('path');

module.exports = {
   <!-- mode指定了打包的模式为：生产环境 -->
   mode:"production",

   <!-- entry是用来配置指定那个文件，是我们的入口文件 -->
   entry:'./src/index.js',

  module:{
    rules:[
        <!-- 转换器安装后，是不需要引入的 -->
        test: /\.css$/,
        use: ["style-loader","css-loader"],
        <!-- 我们先将css转为js，再将js，转为css，所以，先转换的，要写在后面："css-loader" -->
    ]
},

  <!-- plugin 表示数组，每一项代表一个插件，自动在打包的文件中，生成一个 Html的文件-->
  plugins: [new HtmlWebpackPlugin()],
};