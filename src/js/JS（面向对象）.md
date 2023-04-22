# 一.面向对象编辑
1. 内置的构造函数创建
const arr = new Objct()
      arr.name = 'zhangsan'
      arr.mian = 25

2. 字面量创建
const arr = {
  name :'sss',
  nian :25,
  xing : '男'
}

# 二.工厂函数：

             --手动创建对象
             --手动添加成员
             --手动返回对象
 <script>
function sss(index,value){
  const arr = new Object()
      arr.name = 'zhangsan'
      arr.mian = 25
      return arr
}
let brr = sss('shenfen','anhui')
console.log(brr); //{name: "zhangsan", mian: 25}
console.log(brr.name)//zhangsan
 </script>

# 三.构造函数: ----内的属性和方法是私有的
         1.构造函数必须 new关键字调用，首字母大写
         2.构造函数内的this指向new出来的的对象

             --自动创建对象
             --手动添加成员
             --自动返回对象
<script>
  function Person(mane,age){           1.为：构造函数，用来存储p1,p2的属性名和属性值
    this.name = age  
  }
  Person.prototype.show = function(){  2.为：原型，用来存储p1,p2的方法
    console.log('我是构造函数的方法');
  }
  let p1 = new Person('xing','zhangsan') 3.p1的属性存入构造函数内
  console.log(p1.name，p1.age)
  let p2 = new Person('xingbie','wangwu')
  console.log(p2.name)
  p1.show()
  p2.show()
  console.log('我是构造函数的方法')
</script>

# 四.构造函数的弊端:
1. 利用构造函数生成对象，添加属性和方法
2. 构造函数里面的属性和方法都是私有的，不会相同
3. 所以属性放在构造函数中

# 五.原形：----内的属性和方法是共有的
1. 每一个函数天生具有一个原形属性：prototype
2. 而且里面原形的this依然指向实例对象
<script>
  function Person(mane,age){
    this.name = age  
  }
  Person.prototype.show = function(){
    console.log('我是构造函数的方法');
  }
  let p1 = new Person('xing','zhangsan')
  console.log(p1.name)
  let p2 = new Person('xingbie','wangwu')
  console.log(p2.name)
  p1.show()
  p2.show()
  console.log('我是构造函数的方法')
</script>

# 六.梳理面向对象的四种方法
1. 利用系统提供的Object类进行创建--代码冗余
2. 工厂函数--解决代码冗余--对象的创建和返回都是手动
3. 构造函数--自动创建和返回--弊端是里面的属性和方法都是私用的
4. 原型--里面的属性和方法都是公用的

      ----属性用构造函数，
      ----方法用原型prototype

5. 属性和方法：
            ----变量和常量就是属性
            ----函数就是方法
            ----注意this指向

# 七.用面向对象的方法实现Tab选项卡：
<style>
  .father a {
      text-decoration: none;
  }
  a.active {                              
    color: red;
  }
  .father p {
      display: none;
  }   
</style>
<body>
   <div class="father">
    <a href="" class="active">HTML</a>     
    <a href="">CSS</a>
    <a href="">JS</a>
    <p style='display:block'>HTML的全称为超文本标记语言，是一种标记语言。它包括一系列标签，通过这些标签可以将网络上的文档格式统一，使分散的Internet资源连接为一个逻辑整体。HTML文本是由HTML命令组成的描述性文本，HTML命令可以说明文字，图形、动画、声音、表格、链接等。</p>
    <p>层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。</p>
    <p>JavaScript（简称“JS”） 是一种具有函数优先的轻量级，解释型或即时编译型的编程语言。虽然它是作为开发Web页面的脚本语言而出名，但是它也被用到了很多非浏览器环境中，JavaScript 基于原型编程、多范式的动态脚本语言，并且支持面向对象、命令式、声明式、函数式编程范式。</p>
   </div>
</body>
</html>
</html>
<script>
  function Tab(){  3.构造函数的属性
    this.a = document.querySelectorAll('.father a')
    this.p = document.querySelectorAll('.father p')
    4.this指向当前的对象属性
  }
  Tab.prototype.show = function(){
    for(let i=0;i<this.a.length;i++){
      this.a[i].onmouseenter = ()=>{
        for(let j=0;j<this.a.length;j++){
          this.a[j].className = ''
          this.p[j].style.display = 'none'
        }
        this.a[i].className = 'active'
        this.p[i].style.display = 'block'        
      }
    }
  }
  ti = new Tab()   1.ti为：实例对象构造函数
  ti.show()        2.ti为：引用方法
</script>

# 七.构造函数的特点
1. 在函数内是不能判断是否是构造函数，主要看实例对象
<script>
function Person(){
   return '你好'
}
console.log(Person())  //普通函数调用
console.log(new Person())  //构造函数使用

2. 以new操作符调用函数的时候，函数内部会发生变化：

              ###--new内的this指向当前的实例对象

（1） 创建一个空对象，并且this变量会引用该对象
（2） 属性和方法被加入到this引用对象中
（3） 并且最后隐式的返回this

<script>
function Person(name,age){
   this.name = name
   this.age = age
   this.show = function(){
    console.log('构造函数里面的方法')
  } 
}
let p1 = new Person('lisi',20)
console.log(new Person())
</script>

3.如果构造函数的实例对象不传参数的话，可以不加（）
<script>
function Person(name,age){
   this.name = name
   this.age = age
}
let p1 = new Person
</script>
