# 一：Tab选项卡效果： 
    ----鼠标移入a时，a的颜色发生改变，对应的p标签出现，其他p消失
  <style>
    .father a {
        text-decoration: none;
    }
    a.active {                               2.给class名的颜色为红色
      color: red;
    }
    .father p {
        display: none;
    }   
  </style>
  <body>
     <div class="father">
      <a href="" class="active">HTML</a>      1.先给第一个a的起class名
      <a href="">CSS</a>
      <a href="">JS</a>
      <p style='display:block'>HTML的全称为超文本标记语言，是一种标记语言。它包括一系列标签，通过这些标签可以将网络上的文档格式统一，使分散的Internet资源连接为一个逻辑整体。HTML文本是由HTML命令组成的描述性文本，HTML命令可以说明文字，图形、动画、声音、表格、链接等。</p>
                                              3.给第一个p默认出现
      <p>层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。</p>
      <p>JavaScript（简称“JS”） 是一种具有函数优先的轻量级，解释型或即时编译型的编程语言。虽然它是作为开发Web页面的脚本语言而出名，但是它也被用到了很多非浏览器环境中，JavaScript 基于原型编程、多范式的动态脚本语言，并且支持面向对象、命令式、声明式、函数式编程范式。</p>
     </div>
  </body>
  </html>
  </html>
  <script>
    const a = document.querySelectorAll('.father a')
    const p = document.querySelectorAll('.father p')
    for(let i=0;i<a.length;i++){             4.循环a的索引
      a[i].onmouseenter = function (ev){
        var ev = ev ||event
        for(let j=0;j<a.length;j++){         5.循环a的索引
          p[j].style.display = 'none'        6.其他p消失
          a[j].className = ''                7.鼠标不移入其他的a时，class名为空的a没有颜色
        }
        p[i].style.display = 'block'         8.鼠标移入那个a时，对应的p出现
        a[i].className = 'active'          9.鼠标移入那个a时，a的class名为'active'时，颜色出现
        p[i].style.left = ev.clientX +'px'   10.对应的p的X轴位置为：可视窗口的鼠标位置
        p[i].style.top = ev.clientY +'px'    11.对应的p的Y轴位置为：可视窗口的鼠标位置
      }
    }
  </script>

# 二.用面向对象的方法实现Tab选项卡：
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



# 三. 用jQuery：Tab选项卡效果：
 <style>
    *{
      margin: 0;
      padding: 0;
      list-style: none;
    }
    .father {
      position: relative;
      margin: 0 auto;
    }
    ul {
      width: 400px;
      height: 20px;
      border: 1px black solid;
      display: flex;
      justify-content: space-between;
    }
    ul li.active{
      background-color: red;
    }
    ul li {
      height: 20px;
    }
    ul li a {
      font-size: 20px;
      text-decoration: none;
    }
    ol {
      position: absolute;
      left: 0;
      top: 20px;
    }
    ol.show{
      display: block;
    } 
    ol.noshow{
      display: none;
    } 
  </style>
  <body>
    <div class="father">
      <ul>
        <li class="active">
          <a href="#">1111</a>
        </li>
        <li>
          <a href="#">2222</a>
        </li>
        <li>
          <a href="#">3333</a>
        </li>
        <li>
          <a href="#">4444</a>
        </li>
      </ul>
      <ol>
        <li class="show">
          <p>我我我我我我我我我我我我我</p>
        </li>
        <li class="noshow">
          <p>是是是是是是是是是是是是是</p>
        </li>
        <li class="noshow">
          <p>中中中中中中中中中中中中中</p>
        </li>
        <li class="noshow">
          <p>国国国国国国国国国国国国国</p>
        </li>
      </ol>
    </div>
  </body>
  </html>
  <script src="https://code.jquery.com/jquery-3.0.0.min.js"></script>
  <script>
    !function ($){
      const $ali = $('ul li')
      const $oli = $('ol li')
     $ali.on('mouseenter',function(){
        $(this).addClass('active').siblings('li').removeClass('active')
        当前元素.  添加（class名）.兄弟元素（li）.删除（class名）
        $oli.eq($(this).index()).show().siblings('li').hide()
        当前元素对应(ul li 的索引).出现  .兄弟元素.消失
     })
    }(jQuery)
  </script>
