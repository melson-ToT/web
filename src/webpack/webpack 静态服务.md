# 一.启动静态服务器

1. webpackjs.com

2. 点击配置



# 二.DevServer

1. 命令行：webpack-dev-server -D

2. 在 webpack.config.js文件内：

const path = require('path');
module.exports = {
   mode:"production",
   entry:'./src/index.js',
  module:{
    rules:[
        test: /\.css$/,
        use: ["style-loader","css-loader"],
    ]
},
  plugins: [new HtmlWebpackPlugin()],

   <!-- 配置的内容是独立于核心的模块 -->
   compress: true,
   <!-- 输入webpack-dev-server，可直接打开 浏览器-->
   port: 8080,
};