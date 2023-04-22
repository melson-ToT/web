# 一.自定义属性及 Attribute方法：
  <body>
    <div class="father" title="标题文字" date-name="w3c">div标签</div>
  </body>
         1.打印正常属性：
              console.log(a.title)

           非正常属性：getAttribute
              console.log(a.getAttribute('date-name'));

         2.添加属性和属性值：setAttribute
              a.setAttribute('Time','24min');

         3.更改属性值：getAttribute
              a.getAttribute('title','我是新的标题');

         4.删除属性：removeAttribute
              a.removeAttribute('class');
              
<script>
  var a = document.querySelector("div");

  console.log(a.className);   打印正常属性

  console.log(a.title);      打印正常属性

  console.log(a.getAttribute('date-name'));   打印非正常属性

  a.setAttribute('Time','24min');             添加属性和属性值
  console.log(a.getAttribute('Time'));        打印非正常属性

  a.getAttribute('title','我是新的标题');      更改属性值
  console.log(a.getAttribute('title'));       打印非正常属性
 
  a.removeAttribute('class');                  删除属性
  console.log(a.getAttribute('className'));    打印非正常属性
</script>

# 二.自定义属性Attribute方法：给每个li标签加一个  a='1'~a='10'的自定义属性
  <body>
    <ul>              结果为：
      <li>1</li>            <li a="1">1</li>
      <li>2</li>            <li a="2">2</li>
      <li>3</li>            <li a="3">3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
    </ul>
  </body>
</html>
<script>
  var b = document.querySelectorAll("ul li");
  var n = 1
  for (i=0;i<b.length;i++){
    b[i].setAttribute('a',n)
    n++
    console.log(b[i].getAttribute('a'))
  }
</script>

# 或
  var b = document.querySelectorAll("ul li");
  for (i=0;i<b.length;i++){
    b[i].setAttribute('index',i)  
  }


# 三.DOM高级操作--DOM元素类型
      将HTML页面按照节点来划分
  1.元素节点（1） 标签节点
  2.属性节点（2） class、id、title节点
  3.文本节点（3） 内容节点
  4.注释节点（8） 
    nodeName： 节点名称 
    nodeType ：节点类型
    nodeValue：节点的值
    attributes:节点全部集合

  <body>
     <div class="box" id="idbox" title="标题" index-on="fangc"></div>
  </body>
</html>
<script>
  var a = document.querySelector(".box");
  console.log(a.nodeName)    // DIV
  console.log(a.nodeType)    // 1
  console.log(a.nodeValue)   // null
  console.log(a.attributes)  
     // 0: class 1: id 2: title 3: index-on length: 4 class: class id: id index-on: index-ontitle: title __proto__: NamedNodeMap

# js取元素的名称、属性、值的高级写法---换行的空隙也占索引的位置
console.log(a.attributes[1].nodeName)  //id  表示a的所有元素属性结合，对应索引名称为：id
console.log(a.attributes[1].nodeType)  //2   表示a的所有元素属性结合，对应索引类型为：2
console.log(a.attributes[1].nodeValue) //idbox  表示a的所有元素属性结合，对应索引值为：idbox

# 四.js取元素的名称、属性、值的高级写法---换行不占索引的位置
    -----childNodes 考虑换行的空隙和注释，也占索引的位置
    -----children   仅考虑元素,连注释都不考虑
<script>
  var a = document.querySelector("ul");
  console.log(a.childNodes.length)    //21 ----换行的空隙也占索引的位置
  console.log(a.children.length)      //10 ----换行不占索引的位置
</script>  

# 五.节点的高级选取
1.高级选取：
          firstChild:第一个节点（包括空白）   
#         firdtElementChild:第一个节点（不包括空白） 

#   取标签内文本的三种方式
  var a = document.querySelector("li")
  1. a.innerHTML

  var a = document.querySelector("ul");
  2. console.log(a.childNodes[1].childNodes[0].nodeValue)  --childNodes包含空白和索引
        父元素元素内的第二个索引位置--子元素内的第一个索引位置--的值

  3. console.log(a.firstElementChild.innerHTML)
         父元素元素内的第一个索引位置--的内容

#  高级选取：
1.         firstChild:第一个节点（包括空白）   
2.         firdtElementChild:第一个节点（不包括空白）        
3.         lastChild:最后一个节点（包括空白）
4.         lastElementChild：最后一个节点（不包括空白）
5.         previousSibling：上一个兄弟标签的节点（包括空白）
6.         previousElementSibling：上一个兄弟标签的节点（不包括空白）
7.         nextSibling；下一个兄弟标签的节点（包括空白）
8.         nextElementSibling；下一个兄弟标签的节点（不包括空白）

# 如果要取第三个li标签可以：
  var a = document.querySelector("ul")
  console.log(a.firstElementChild.nextElementSibling.nextElementSibling)//<li>3</li>


# 六.基本控制结构元素的获取
  var a = document.querySelector("body");

  var a = document                      获取document元素

          document.body                 获取body元素

          document.documentElement      获取HTML标签元素

          document.title                获取标题元素

#         parentNode                    获取当前元素的父元素
                      var a = document.querySelector("li");
                      console.log(a.parentNode)  //  <ul>...</ul>

          Style.display                 获取css中的display

          innerHTML                     获取元素的文本

# 七.微博发布案例

  
  
 