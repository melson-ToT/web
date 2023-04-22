#    一.模块化的意义
   1.考虑的问题:冲突和依赖(不是业务逻辑，js代码优秀的写法)
   2.函数编程---->闭包---->命名空间---->模块化编程
   2.1.函数编程：减少冲突，看不出依赖
   var name = 'zhangsan';
   var name = 'lisi';
   下面覆盖上面，采用函数形成局部作用域，减少冲突
   function fn() {
     var name = 'zhangsan';
     console.log(name);
   }
 
   function fn1() {
     var name = 'lisi';
     console.log(name);
   }
 
   function fn() {
     var name = 'wangwu';
     console.log(name);
   }
   如果都是函数，依然存在冲突的
 
   2.2.闭包：比函数更能减少冲突，闭包有弊端，变量常驻内存。看不出依赖
   !function () {
     function fn() {
       var name = 'zhangsan';
       console.log(name);
     }
 
     function fn1() {
       var name = 'lisi';
       console.log(name);
     }
     fn();
     fn1();
   }();
   !function () {
     function fn() {
       var name = 'wangwu';
       console.log(name);
     }
     fn();
   }();
 
   2.3.命名空间，使用命名形成区别，减少冲突，看不出依赖。
   function TB_movie_item1_version3_tools_getDate() {
 
   }
 
   # 二.模块化编程
   1.模块化编程解决冲突和依赖
   2.模块化的意义
   就是指将页面根据内容的关联性分解成不同的且相互独立的模块进行开发
   每个模块之间没有必然的联系，互不影响，想要什么功能，就加载什么模块
   每个 JavaScript 文件就是一个独立的模块 - 最重要的
   大家必须以同样的方式编写模块，否则达不到预想的效果 - 方便复用
 
   三.模块化的历史以及模块化的规范
   1.commonJS：2009年提出第一个模块化的规范，但是这个规范适合于后端，不是前端的规范，Nodejs实现了这个规范。
   2.amd：参考commonJS规范出现的，属于前端的规范，异步模块定义，require.js实现了这个规范，想使用必须下载require.js
   3.cmd：前端的规范，中国淘宝的花名叫做玉伯的提出的,通用的模块定义，sea.js实现了这个规范，想使用必须下载sea.js
 
   规范的核心思想：每个JavaScript文件就是一个独立的模块，定义模块，调用模块，配置模块。
 
   
   四.ES6的模块化
   在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。
   前者用于服务器，后者用于浏览器。
   ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。
 
</script>
<!-- 
<script src="zhangsan.js"></script>
<script src="lisi.js"></script>
<script src="wangwu.js"></script> 
-->


# 三.  // ES6的模块化开发(每个JavaScript文件就是一个独立的模块)
  // 只要是模块化开发，关心的就是定义模块，调用模块，以及配置模块
 
  // 1.定义模块(导出模块,暴露模块)
  // export命令导出模块,知道导出的模块名称
  // export default 暴露一个变量或者函数，调用的时候自定义名称，一个模块只能有一个默认输出，因此export default命令只能使用一次。
 
  // 2.调用模块
  // import命令导入模块，必须知道导出模块的名称，可以修改名称
  // 利用as语句修改导出的模块名称。
  // import { $ as ele, queryString } from './mod_tool.js';
 
  // 3.配置模块
  // 配置本地路径(./)
 
  // 4.html文件引入模块
  // 浏览器加载 ES6 模块，也使用script标签，但是要加入type="module"属性
  // 浏览器对于带有type="module"的script都是异步加载，不会造成堵塞浏览器
  // 如果网页有多个script type="module"，它们会按照在页面出现的顺序依次执行。



# 四.模块化的写法：

# 1.建立一个导出的js文件

const arr = [1,2,3,4,5]
let obj={
  name:'zhansan',
  age:'男',
  sex:20
}
function fn(){
  console.log('我是函数');
}
class Fa{
  constructor(box){
    this.box = box
  }
  init(){
    console.log(this.box);
  }
}
export{  // export命令导出模块，固定写法
  arr,
  obj,
  fn,
  Fa
}


# 2.建立一个导入的js文件

import{arr,obj,fn,Fa} from "./daochu.js"      //import命令导入模块,固定写法；              "./daoru.js"是导出的文件

console.log(arr);            
console.log(obj);
fn()
new Fa('里古拉斯').init()


# 3.引入导入的文件到html文件
  <script src="./daoru.js" type="module"></script>
  引入文件时，src内，./是本目录，一定要加type属性，属性值为module，固定写法



# 五.模块化的应用：
