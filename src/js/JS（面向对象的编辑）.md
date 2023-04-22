# 一.面向对象和面向过程的区别：
1. 面向对象：以对象为中心，通过类实现具有相同属性和方法的对象
2. 面向过程：函数式编辑，将事件按照顺序一步步的完成
3. 面向对象不是语法，是一个思想，是一种编辑模式

# 二.创建对象：
1. 利用系统提供的Object类进行创建--代码冗余
2. 工厂函数--解决代码冗余--对象的创建和返回都是手动
3. 构造函数--自动创建和返回--弊端是里面的属性和方法都是私用的
4. 原型--里面的属性和方法都是公用的

# 三.构造函数和原形(prototype)：
1. 构造函数：
          --内的属性和方法都是私有的
          --首字母大写，new调用，this指向实例对象

2. 原形(prototype)：
            --内的属性和方法都是公有的
            --this指向实例对象

3. 构造函数放置：属性

4. 原形(prototype)放置：方法

# 如：
  <script>
   function Fath(){
    放置属性
   }
   Fath.prototype.init = function(){
    放置方法
   }
   new Fath().init() 执行
  </script>

# 四.构造函数的原形：
<script>
  function Fath() {
    this.name = name
  }
  Fath.prototype.init = function () {
    console.log('我是原形的方法');
  }
  Object.prototype.hehe= function () {
    console.log('我是Object的方法');
  }
  let p1 = new Fath()//p1为：实例对象，new Fath()为：构造函数
  p1.init()//为:p1调用init的方法
  p1.hehe()//为：p1调用hehe的方法
</script>

# 五.为什么实例对象可以访问原形的方法：
1. 如果实例对象调用属性和方法，先找构造函数里面的，如果有，就直接使用
2. 如果构造函数里面没有，就会继续找构造函数原形（prototype）上面的属性和方法，如果有，就直接使用，如果没有
3. 就会继续找Object.prototype上面的属性和方法，如果有，就直接使用，如果没有，直接报错

# 六.原形链：__proto__
1. 原型链的概述：实例对象与构造原形（prototype）之间的连接，依靠内置原形（__proto__）来完成
2. 原型链的过程：
              实例对象调用属性和方法，先找构造函数里面的，如果有，就直接使用，如果构造函数里面没有，就会继续找构造函数原形（prototype）上面的属性和方法，如果有，就直接使用，如果没有，就会继续找Object.prototype上面的属性和方法，如果有，就直接使用，如果没有，直接报错
 
# 七.constructor：只针对构造函数
1. 对象的__proto__里面有一个成员叫做constructor
2. 这个属性就是指当前对象所属的构造函数
<script>
  function Fan(){
    '我是构造函数'
  }
  let p1 = new Fan()
  console.log(p1.constructor);// ƒ Fan(){'我是构造函数'}
</script>

# 八.instanceof属性：从属关系
          --检查一个对象是否是某个构造函数的实例对象
<script>
  function Fan(){
  }
  let p1 = new Fan()
  console.log(p1 instanceof Fan);//true
  console.log(p1 instanceof Object);//true 因为一切皆对象
</script>

# 九.hasOwnproperty():看是不是实例对象构造函数下面的属性，不会继承原型链上面的
<script>
  function Fan(){
    this.name = 'zhangsan'
  }
  Fan.prototype.init = function(){
    'lisi'
  }
  let p1 = new Fan()
  p1.init()
  console.log(p1.hasOwnProperty('name'))//true 只会检查实例对象构造函数里面的属性
  console.log(p1.hasOwnProperty('init'))//false
</script>

# 十.扩展in运算符，来自于for in里面的in运算符，也可以检查属性是否是实例对象的属性（但包括原型链）
<script>
  function Fan(){
    this.name = 'zhangsan'
  }
  Fan.prototype.init = function(){
    'lisi'
  }
  Object.prototype.age = function(){
    'wangwu'
  }
  let p1 = new Fan()
  p1.init()
  p1.age()
  console.log('name' in p1)//true
  console.log('init' in p1)//true
  console.log('age' in p1)//true
</script>

# 十一.toString():
1. 系统对象下都是自带的，
2. 自己写的通过原型链继承Object,可以转成字符串
<script>
let a = [1,2,3]
console.log(a.toString())//1,2,3
</script>

### 十二.类型的判断：
1. typeof:适合判断基本类型（number/string/boolean）

2. constructor:适合判断引用类型（函数或构造函数）
<script>
  function Fan(){
    '我是构造函数'
  }
  let p1 = new Fan()
  console.log(p1.constructor);// ƒ Fan(){'我是构造函数'}
</script>

3. instanceof：适合判断数据类型

4. toString:适合判断所属的类型:
<script>
console.log(Object.prototype.toString.call('hello'));//[object String]
console.log(Object.prototype.toString.call(123));//[object Number]
console.log(Object.prototype.toString.call(true));//[object Boolean]
console.log(Object.prototype.toString.call(null));//[object Null]
console.log(Object.prototype.toString.call(undefined));//[object Undefined]
console.log(Object.prototype.toString.call([]));//[object Array]
console.log(Object.prototype.toString.call({}));//[object Object]
console.log(Object.prototype.toString.call(function(){}));//[object Function]
console.log(Object.prototype.toString.call(new Date));//[object Date]
console.log(Object.prototype.toString.call(/\d/));//[object RegExp]
</script>

# 总结：
1. 如果是基本类型，可以采用typeof
2. 如果是引用类型，使用constructor
3. 无法确定类型，或者一次性确定，使用toString









# 十二.面向对象混合开发的放大镜效果
<style> 
  *{
    margin: 0;
    padding: 0;
  }
  .father {
    margin: 50px 0 0 50px;
  }
  .box {
    width: 300px;
    height: 300px;
    float: left;
    position: relative;
  }
  .xiaotu {
    width: 100%;
    height: 100%;
  }
  .xijing {
    width: 200px;
    height: 200px;
    background-color: blue;
    opacity: 0.3;
    position: absolute;
    top: 0;
    left: 0;
    visibility:hidden;
  }
  .dajing {
    width: 400px;
    height: 400px;
    position: relative;
    overflow: hidden;
    float: left;
  }
  .datu {
    width: 600px;
    height: 600px;
    position:absolute;
    top: 0;
    left: 0;
  }
  </style>
  <body>
    <div class="father">
      <div class="box">
        <img src="../img/女好骚.png" alt="" class="xiaotu">
        <div class="xijing"></div>
      </div>
      <div class="dajing">
        <img src="../img/女好骚.png" alt="" class="datu">
      </div>
    </div>
  </body>
  </html>
  </html>
  <script>
   function Fath(){
    this.father = document.querySelector('.father')
    this.box = document.querySelector('.box')
    this.xiaotu = document.querySelector('.xiaotu')
    this.xijing = document.querySelector('.xijing')
    this.dajing = document.querySelector('.dajing')
    this.datu = document.querySelector('.datu')
   }
   Fath.prototype.init = function(){
    this.box.onmouseenter = ()=>{
      this.xijing.style.visibility = 'visible'
      this.box.onmousemove = (e)=>{
        let leftvalue = e.clientX - this.father.offsetLeft - this.xijing.offsetWidth/2
        let topvalue = e.clientY - this.father.offsetTop - this.xijing.offsetHeight/2
        if(leftvalue <=0){
          leftvalue = 0
        }else if(leftvalue >= this.xiaotu.offsetWidth - this.xijing.offsetWidth){
          leftvalue = this.xiaotu.offsetWidth - this.xijing.offsetWidth
        }
        if(topvalue <=0){
          topvalue = 0
        }else if(topvalue >= this.xiaotu.offsetHeight - this.xijing.offsetHeight){
          topvalue = this.xiaotu.offsetHeight - this.xijing.offsetHeight
        }
        this.xijing.style.left = leftvalue + 'px'
        this.xijing.style.top = topvalue + 'px'
        this.datu.style.left = -leftvalue*(this.datu.offsetWidth / this.xiaotu.offsetWidth) + 'px'
        this.datu.style.top = -topvalue*(this.datu.offsetWidth / this.xiaotu.offsetWidth) + 'px'
      }
    }
    this.box.onmouseleave = ()=>{
      this.xijing.style.visibility = 'hidden'
    }
   }
   new Fath().init()
  </script>



    