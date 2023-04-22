# 一：js 的方法：
1. 动态方法：
          内置构造函数基本上都有原形方法，给实例对象使用的：
          push、pop、split...

2. 静态方法：
          以构造函数或类名开头的使用，不能给实例对象使用，必须通过构造函数名或类名调用
          Array.isArray  检查是否是数组
          Object.keys    检查是否是对象

3. class实现方式:
          构造函数的原形，都会被实例对象继承，如果在一个方法前，加上 static 关键字，就表示该方法不会被实例对象继承，而是直接通过构造函数的原形来调用，这就称为：静态方法
<script>
  class Fan{
    constructor(){
      this.name = 'zhangsan'
    }
    init_1(){
      'lisi'
    }
    static init_2(){
      'wangwu'
    }    
  }
  let p1 = new Fan()
  console.log(p1.init_1)//ƒ (){'lisi'}
  console.log(p1.init_2)//undefined
  console.log(Fan.init_2)//ƒ init_2(){'wangwu'}
</script>

# 二.面向对象的封装：
封装：固定的功能，经常使用的代码通风函数封装，减少代码的冗余

# 三.面向对象继承的概述：
1. 子类继承父类，但子类不能影响父类
2. 实例对象的多个构造函数或原形，内有相同的属性和方法，可以采用继承来减少代码的冗余
3. 如果继承的构造函数和被继承的构造函数都具有相同的属性，那就无需继承

# 四.面向对象的继承
（一）混合继承
    1.构造函数的继承
<script>
  function Fan(name,xing,nian){
      this.name = 'zhangsan'
      this.xing = 'lisi'
      this.nian = '20'
    }
  function Fsn(name,xing,nian,age){
      Fan.call(this,name,xing,nian)
      //call是函数下面的方法：第一个参数表示this的指向，从第二个开始，表示函数本身的参数
      //也可以用 Fan.apply(this,arguments)：第一个参数表示this的指向，arguments表示数组或类数组
      this.age = 'lisi'
    }
  let p1 = new Fan()
  let p2 = new Fsn()
  console.log(p1)// Fan {name: "zhangsan", xing: "lisi", nian: "20"}
  console.log(p2)// Fsn {name: "zhangsan", xing: "lisi", nian: "20", age: "lisi"}
</script> 

    2.原形的继承


（二）class继承
1. 构造函数继承:
              ----extends:关键字继承，让子类继承父类的属性和方法
              ----super：关键字当做函数使用时，就表示父类的构造函数
<script>
  class Fan{
    constructor(name,age,tim){  //所需要的形参
      this.name = name
      this.age = age
      this.tim = tim
    }   
  }
  class Fsn extends Fan{  // class Fsn 继承 Fan的属性和方法
    constructor(name,age,tim,xing){ //所需要的实参
      super(name,age,tim)  // 被继承的（形参）
    //在子类的构造函数中，只有调用super()之后，才可以使用this关键字，否则会报错
    //这是因为子类实例的构建，必须先完成父类的继承，只有super()方法才能让子类继承父类，才拥有this
      this.xing = xing  // 自己的属性
    }
  }
  let p1 = new Fan('zhangsan','lisi','wangwu') //实参
  let p2 = new Fsn('zhangsan','lisi','wangwu','laoliu') //实参
  console.log(p1)
  console.log(p2)
</script>

2. 原形继承：
<script>
  class Fan{
    constructor(name,age,tim){
      this.name = name
      this.age = age
      this.tim = tim
    }   
    init(){     //原形                    
      document.onmousemove = ()=>{
      }
    }
  }
  class Fsn extends Fan{
    constructor(name,age,tim,xing){
      super(name,age,tim)
      this.xing = xing
    }
    inot(){
      document.onmousemove = ()=>{
        `${super.init()}`  //继承父类的方法：super.init()父类的原形方法
      }      
    }
  }
  let p1 = new Fan('zhangsan','lisi','wangwu')
  let p2 = new Fsn('zhangsan','lisi','wangwu','laoliu')
  p1.init()
  p2.inot()
  console.log(p1)
  console.log(p2)
  console.log(p1.init)
  console.log(p2.inot)
</script>


3. 原形继承：带入事件
<script>
  class Fan{
    constructor(name,age,tim){
      this.name = name
      this.age = age
      this.tim = tim
    }   
    init(){
      document.oncontextmenu = ()=>{//右键点击
        document.body.style.backgroundColor= 'red'
      }
    }
  }
  class Fsn extends Fan{
    constructor(name,age,tim,xing){
      super(name,age,tim)
      this.xing = xing
    }
    inot(){
      document.onclick = ()=>{//左键点击
        document.body.style.backgroundColor= 'blue'
        super.init()//带入继承的原形方法
      }      
    }
  }
  let p1 = new Fan('zhangsan','lisi','wangwu')
  let p2 = new Fsn('zhangsan','lisi','wangwu','laoliu')
  p1.init()
  p2.inot()
  console.log(p1)
  console.log(p2)
  console.log(p1.init)
  console.log(p2.inot)
</script>

# 所打印的结果：
Fan {name: "zhangsan", age: "lisi", tim: "wangwu"}
Fsn {name: "zhangsan", age: "lisi", tim: "wangwu", xing: "laoliu"}
init(){
      document.oncontextmenu = ()=>{
        document.body.style.backgroundColor= 'red'
      }
    }
inot(){
      document.onclick = ()=>{
        document.body.style.backgroundColor= 'blue'
        super.init()
      }      
    }


# 五.Object 和 Function: --对象的类 和 Function的类

1. 函数属于对象，同时函数也是对象的构造器

2. 函数:
       ----函数有一个属性：length             参数的长度
       ----函数欧两个对象：this，argument     指向第一个，arguments：数组或类数组
       ----函数的三个方法（call/apply/bind）

3. 原形下面有两个属性：
                ----constructor
                ----__proto__
类的__proto__  ===  Function.constructor
对象的__proto__  ===  Object.constructor