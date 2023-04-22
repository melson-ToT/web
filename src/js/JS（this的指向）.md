# 一：this指向：
             --谁调用，指向谁，没有调用，指向Window

# 二.构造函数（类）：首字母大写，new关键字调用
        --构造函数的this指向类创建出来的对象（又称实例对象）
    
# 三.函数对象的属性和方法:
     ----构造函数的3个方法会改变this的指向
     1.fn.call(obj,3,5)
     2.fn.apply(obj,[3,5])
     3.fn.bind(obj,3,5)() 

1. call：this指向call内的第一个参数,从第二个参数开始，就是函数本身的参数，用逗号隔开
       var obj = {a=1}
       functoin fn(n1,n2){
        n1+n2
       }
       fn.call(obj,3,5)
       此时this指向obj

2. apply:this指向apply内的第一个参数,第二个参数时数组，数组项就是函数本身的参数
       fn.apply(obj,[3,5])

3. bind：this指向bind内的第一个参数,从第二个参数开始，就是函数本身的参数，用逗号隔开，返回函数体，需要再次触发
       fn.bind(obj,3,5)() ---加（）才会触发

# 案例1；点击li时，延时1秒才会触发，使li的内容改变：
#      ----由于演示定时器在点击事件内，所以this的指向会发生变化

方法一：
  <body>
     <li>1111</li>
     <li>1111</li>
     <li>1111</li>
     <li>1111</li>
  </body>
  </html>
  </html>
  <script>
  var li = document.querySelectorAll('li')
  for(i=0;i<li.length;i++){ 
     li[i].onclick = function(){
      var _this = this                            1.先给this一个变量存起来
      var time = window.setTimeout(function (){
        _this.innerHTML='2222'                    2.调用时，再给它
      },2000)  
    }
  }
</script>

方法二：
  <script>
  var li = document.querySelectorAll('li')
  for(i=0;i<li.length;i++){ 
     li[i].onclick = function(){
      var time = window.setTimeout(function (){
        this.innerHTML='2222'
      }.bind(this),1000)         .bind(this)，.bind为绑定事件，此时.bind绑定为li[i]
    }
  }
</script>

# 四.JSON对象的介绍：
                ----JSON是最好的前后端交互方式
  1.--JSON的特点：
                JSON的组成：简单值+'对象'+'数组'
                JSON里面字符串需要添加双引号
                JSON没有var、分号、注释等JS相关的语法

  2.--JSON的静态方法：----非常重要：
                JSON.parse()      :用于从一个字符串中解析出JSON对象，具有检测功能
                JSON.stringify()  :将对象转换成JSON格式的字符串

# 案例1：
      ----利用JSON的.parse()方法，将后端的数据进行处理

  var arr = '["zhangshan","lisi","wangwu","laoliu"]'  1.后端给的JSON
  var brr = JSON.parse(arr)           2.利用JSON的.parse()方法，转换为字符串
  var str = ''                        3.建立一个空数组或对象
  brr.forEach(function (value){       4.循环brr的value值
     str += '<li>'+ value +'</li>'    5.str的每一项 = 每一个li标签内，brr的value值
  })
  document.body.innerHTML = str       6.body的内容 = str
</script>

# 案例2；   将对象转换成JSON格式的字符串 
var arr = {
    a : 1,
    b : 2,
    c : 3 
  }
  var brr = JSON.stringify(arr)
  console.log(brr)           // {"a":1,"b":2,"c":3}

# 注意：对象如果进行传输或者存储，一定要将对象转为字符串格式的存在，数组则可以省略

# 五.ES6语法介绍：
      （一）1.let：所声明的变量就‘绑定’这个区域，不再受外部的影响,{}内使用，不可重复声明
                  ----又称代码块内使用（只在这块的区域内使用）

            2.const：常量，不可改变（能使用常量尽量不用变量），不可重复声明
                比如：1.获取元素
                     2.封装元素

# 案例：Tab选项卡效果： 
    ----鼠标移入a时，a的颜色发生改变，对应的p标签出现，其他p消失
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
    const a = document.querySelectorAll('.father a')
    const p = document.querySelectorAll('.father p')
    for(let i=0;i<a.length;i++){
      a[i].onmouseenter = function (){
        for(let j=0;j<a.length;j++){
          p[j].style.display = 'none'
          a[j].className = ''
        }
        p[i].style.display = 'block'
        a[i].className = 'active'
      }
    }
  </script>

# 六.变量的解构赋值：
     1.数组的解构赋值：--数组的格式要统一
           ----将数组arr，封装函数，输出数字数组的最大值、最小值、length属性
<script>
  let arr = [12,5,88,23,74,100,]
  function getvalue(arr){
    arr.sort(function(a,b){
      return a-b                                1.数组内的数字按小到大的排序
    })
    return [arr[arr.length-1],arr[0],arr.length]
    2.返回最小值，最大值和长度，此时getvalue(arr)只有这3个值
  }
  let [maxvalue,minvalue,len] = getvalue(arr)  3.用三个自定义的名称来结构getvalue(arr)的值
  console.log(maxvalue,minvalue,len)           4.取到想要的值
  </script>

   2.对象的解构赋值：
                 ----对象的变量名和属性名要一致
                 ----获取时，通过属性名来获取
                 ----如果需要修改属性名，通过：来实现
                        a:b----得到值的时后者      
  <script>
  let obj = { 
    mane:'zhangsan',
    xingbie:'男',
    nianln:'20'
  }
  let {mane,xingbie,nianln} = obj
  console.log(mane,xingbie,nianln);
  </script>     

# 七.合并数组
           ...来合并       
  <script>
     let arr = [a=1,b=2,c=3] 
     let brr = [d=4,f=5,e=6]
     let crr = [...arr,...brr]
     console.log(crr) //[ 1 2 3 4 5 6 ]
  </script>

# 八.合并对象
  <script>
     let arr = {a:1,b:2,c:3}
     let brr = {d:4,f:5,e:6}
     let crr ={...arr,...brr}
     console.log(crr) //{a: 1, b: 2, c: 3, d: 4, f: 5, …}
  </script>

# 九.数据对插
  <script>
     let arr = [{a: 1}, {b: 2}, {c: 3}]
     let brr = [{i: 4}, {j: 5}, {k: 6}]
     let crr = []
     for(let i=0;i<arr.length;i++){
       let drr = {...arr[i],...brr[i]}
       crr.push(drr)
     }
     console.log(crr);
  </script>

# 十.取最大值，最小值
  <script>
    let arr = [12,5,88,23,74,100]
    let brr = Math.max(...arr)
    let crr = Math.min(...arr)
  </script>

# 十一.模板字符串
             ----是增强版的字符串，用反引号``标识，可以用于普通字符串使用，也可以定义第一行字符串，或者在字符串中嵌入变量${}--非常重要

# 案例1：数组渲染的核心
  <script>
    let arr = ''
    const brr = [111,222,333,444]
    for(let i=0;i<brr.length;i++){
      arr+=`
      <div class="box">
      <ul>
        <li>
          <a href="#">${brr[i]}</a>
        </li>
      </ul>
    </div>
    `
    }
    document.body.innerHTML = arr
  </script>

# 案例2：对象渲染的核心
  <script>
    let obj = {
      name : 'zhangsan',
      sex : '男',
      aeg :100,
      show:function(){
        return `我的姓名是${this.name},我的年龄是${this.aeg},我的性别是${this.sex},`
      }
    }
    console.log(obj.show());
  </script>

# 十二.箭头函数：--箭头函数内的this于来自父级，如果没有，则指向wondow，不可以用new

  const som = function(a){
    return a
  }
  console.log(som('5'));

  const son = a=>a
  console.log(son('5));

  const sos = (a,b)=>a+b
  console.log(sos(3,5));

  const sos = (a)=>{
   a++
   return a
  }
  console.log(sos(3));

# --箭头函数内的this于来自父级，，不会再改变 --如果没有，则指向wondow
  <body>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
 </body>
 </html>
 </html>
 <script>
 var li = document.querySelectorAll('li')
 for(i=0;i<li.length;i++){ 
    li[i].onclick = function(){
     var time = window.setTimeout(()=>{
       this.innerHTML='2222'             1.此时的this指向父级，不会再改变      
     },1000)  
   }
 }
</script>

# 十三.数组的扩展方法：
1. Array.from()：方法用于将对象转为真正的数组或类数组
               条件：
                   1.对象的名称要以索引开始
                   2.最后要有length名和length值
<script>
let obj = {
  0:'name',
  1:20,
  2:'男',
  length:3
}
let arr = Array.from(obj)
console.log(arr)
</script>


2. Array.fo()方法用于将一组值转换为数组
   console.log(Array.of(1,2,3,4,5))

3. fill()方法使用给定值，填充一个数组（索引位置）
 <script>
  let arr = [1,2,3,4,5,6]
  console.log(arr.fill('zhangsan',2,5))
</script>
(6) [1, 2, "zhangsan", "zhangsan", "zhangsan", 6]

# 十四.对象的扩展方法：
1. Object.assign()用于对象的合并,如果属性名有重名，则前面的属性名会被覆盖
 <script>
  let obj1= {
    a:1,
    b:2,
    c:3
  }
  let obj2= {
    d:4,
    e:5,
    f:6
  }
  let obj3= {
    g:7,
    h:8,
    i:9
  }
  let obj = Object.assign({},obj1,obj2,obj3)
  console.log(obj)  //{a: 1, b: 2, c: 3, d: 4, e: 5, …}
</script>

2. Object.keys()获取对象的所有属性名，返回一个数组
 <script>
  let obj= {
    a:1,
    b:2,
    c:3
  }
  console.log(Object.keys(obj))  //(3) ["a", "b", "c"]
</script>

3. Object.values()获取对象的所有属性值，返回一个数组
 <script>
  let obj= {
    a:1,
    b:2,
    c:3
  }
  console.log(Object.values(obj)) //(3) [1, 2, 3]
</script>

