# 一 数组的核心 :
1.两种方式创建数组 2.数组的 length 属性和下标索引 3.数组的方法:
--转换方法：toString()转字符串
--检测方法：array.isArray()
--俴方法：后进先出，push 后面追加，pop 后面删除，后进的先删除
--队列方法：先进先出，unshift 前面追加，shift 前面删除，先进的先删除
--重排序方法：reverse sort
--操作方法：concat slice splice
--转换方法：join
--位置方法：indexOf lastIndexOf includes
--迭代方法：every some filter map forEach
--归并方法：reduce reduceRight

# 二.js 的核心组成部分

1.核心（ECMAScript）；描述了该语音和基本对象（es5、es6）

2.浏览器对象模型（BOM）:描述与浏览器进行交互的方法和接口
----js 代码依靠浏览器进行解释的，必须掌握浏览器的一些特性
----BOM 和网页内容没有一点关系
----BOM 的核心是 window 对象，window 对象下面的子对象
----window 的双重角色： 1.表示 js 里面的全局对象 2.表示浏览器打开的一个窗口

3.文档对象模型（DOM）:描述处理网页内容的方法和接口
----DOM 和网页内容有关
----DOM 操作标签，标签里面的属性，标签里面的内容

# 三.window 内置对象及方法

1.window 的子对象
---location 对象 用来操作网页的地址栏
地址栏的组成：
网站的网址（域名）+路径（/文件的位置）+？拼接数据（多条数据&符号连接）+#哈希值（hash）
https://www.baidu.com/play.?video#E5%AE%9A%E5%9.#mp4&t=-1
域名：https://www.baidu.com
路径：/play.video
数据:?video#E5%AE%9A%E5%9. --重要
哈希值（页面跳转使用）：#mp4&t=-1 路由的核心 --最重要

    location.href属性：读写地址栏所有的内容，地址栏的中文会自动转化编码
            consolr.log(window.location.href)--读
                 file:///D:/1/html/%E7%BB%83%E4%B9%A0.html
            window.location.href='http://jd.com'--写

    location.search属性：读取地址栏?后面的数据
           consolr.log(window.location.search)//?video

    location.hash属性：读取地址栏#后面的数据
           consolr.log(window.location.search)//#E5%AE%9A%E5%9.

    location.assign()方法：设置地址栏
           window.location.assign('http://jd.com')

    location.reload(true)方法,刷新页面，可以设置参数为true
           alert(1)
           location.reload(true)//刷新

# 四页面跳转案例
    document.onclick=function(){      点击页面
    location.assign('http://jd.com')  跳转到'http://jd.com'
}

# 五.window BOM 的相关的事件和操作
1.window 的相关操作--事件不能省略 window
    (1)onload 事件：页面加载完成后触发此事件（DOM 结构，图片等内容）
    --onload 事件解决代码顺序问题，onload 后面的代码等待结构或者网页内容加载完成之后再执行
    --事件不能重复应用，页面不能出现两个相同的事件，否则后面的会覆盖前面的
window.onload=function(){
    --页面刷新后触发里面的内容
}

(2)onscroll 事件：拖动浏览器的滚动条触发此事件，而且此事件的触发频率很高
  document.documentElement.scrollTop  表示：获取html
  document.body.scrollTop  表示：获取body
</html>
<script>
  var a=document.querySelector('body')
  window.onscroll=function(){
    var top = document.documentElement.scrollTop || document.body.scrollTop
    console.log(444, top);//打印数据
    if (top >= 1000) {
      a.style.background='pink'
    } else {
      a.style.background='#fff'
    }
  }
</script>

(3)onresize 事件：浏览器窗口缩放所触发的事件，触发的频率很高
#    ---这里的缩放指的是：浏览器中可视的窗口（看得见的区域）
#     window.onresize=function(){
#         console.log(document.documentElement.clientWidth,document.documentElement.clientHeight)
        }

# 滚动条拉倒底部，点击documen后，页面跳转到顶部
   点击document,滚动条的top值为0
    document.onclick=function(){      
       document.documentElement.scrollTop=0
}

## 六.DOM的概念：
        'Document Object Model'的首字母缩写，即文档对象模型，用来描述一个层次的节点数，允许开发人员进行获取，增删改查页面的某一个部分元素

  <a href="http://www.baidu.com" target="_blank" title="链接的标题">百度</a>

  1.Element:元素对象
     Attribute:元素内的属性:
                      href="http://www.baidu.com"
                      target="_blank"
                      title="链接的标题"
     Text:百度，元素对象里面的文本内容

  2.查找HTML对象：
            一个标签，querySelector取元素方法：
            var a=document.querySelector('.div')

            多个一样的标签，querySelector取某个单个元素方法：
            var a=document.querySelector('div:nth-of-type(2)')

            多个一样的标签，querySelectorAll取全部元素方法：
            var a=document.querySelectorAll('div')

            多个一样的标签，querySelectorAll取单个元素方法
            var a=document.querySelectorAll('div')[3]

  3.获取HTML元素对象的属性:  (默认属性)
            
            ----通过 .或[]来操作符进行读写

            <a href="http://www.baidu.com" target="_blank" title="链接的标题">百度</a>
            var biaoqian=document.querySelectorAll('a')

            1.获取属性
            console.log(biaoqian.hrdf)//href="http://www.baidu.com"
            ----注意：如果自定义的属性来操作，则系统报错：undefined(属性不存在)

            2.修改属性
            biaoqian.hrdf="http://jd.com"//修改了a标签里面的网址

  4.获取HTML元素对象的内容：
              <div>11111</div>
              var a = document.querySelectorAll('div')

#           1.innerHTML:   获取包括自身标签的全部内容--重点（渲染的核心）
                        a.innerHTML//11111

            2.outerHTML:   获取标签内文本的全部内容
                        a.innerHTML//<div>11111</div>

            3.outerText：  获取标签文本内容
                        a.innerText//11111

# 七.获取css样式的值：
                --利用元素对象属性获取css的常用属性:offset （盒模型）
#                     （盒模型）:border+padding+width+height
    div {
      width: 100px;
      height: 100px;
      background-color: pink;
      text-align: center;
      line-height: 50px;
      margin: 10px 10px;
      box-sizing: border-box;
    }
  </style>
  <body>
     <div>我们的祖国</div>
  </body>

  1.offsetwWidth:获取css内元素对象的宽                 
        var a = document.querySelector("div");
        console.log(a.offsetWidth);//100

  2.offsetwHeight:获取css内元素对象的高                
        var a = document.querySelector("div");
        console.log(a.offsetHeight);//100

  3.offsetwTop:获取css内元素对象margin的向下位置       
        var a = document.querySelector("div");
        console.log(a.offsetTop);//10

  4.offsetwLeft:获取css内元素对象padding的向右位置    
        var a = document.querySelector("div");
        console.log(a.offsetLeft);//10

  5.offsetwParebt:获取css内元素对象父级定位            

# 八.可以获取也能修改的css元素对象值的方法：
    div {
      width: 100px;
      height: 100px;
      background-color: pink;
      text-align: center;
      line-height: 50px;
      margin: 10px 10px;
      box-sizing: border-box;
    }
  </style>
  <body>
     <div>我们的祖国</div>
  </body>

#  var a = document.querySelector("div");
   a.onclick=function(){
     a.style.width='200px'
     a.style.background='#000'  或a.style.backgroundColor='#000'
     a.style.color='#fff'
     a.innerHTML='张飞'
     a.style.marginLeft='100px'
# console.log(getComputedStyle(a).width)            打印当前a在css中width的值
# console.log(getComputedStyle(a).backgroundColor)  打印当前a在css中backgroundColor的值
# console.log(getComputedStyle(a).color)            打印当前a在css中color的值
# console.log(getComputedStyle(a).innerHTML)        打印当前a在css中innerHTML的值
# console.log(getComputedStyle(a).marginLeft)       打印当前a在css中marginLeft的值
}

# console.log(getComputedStyle(a).width)            打印点击事件之后a在css中width的值
# console.log(getComputedStyle(a).backgroundColor)  打印点击事件之后a在css中backgroundColor的值
# console.log(getComputedStyle(a).color)            打印点击事件之后a在css中color的值
# console.log(getComputedStyle(a).innerHTML)        打印点击事件之后a在css中innerHTML的值
# console.log(getComputedStyle(a).marginLeft)       打印点击事件之后a在css中marginLeft的值

## 九浏览器的兼容写法：
  --getComputedStyle   标准
  --currentStyle       非标准

function getStyle(obj,attr){
  if(getComputedStyle){
    return getComputedStyle(obj).attr
  }
  else{
    return obj.currentStyle.attr
  }

# 十，创建、添加、删除、克隆、替换
1.创建元素对象：
 document.createElemrnt('元素对象的名称')
 var aImg = document.createElemrnt('img')
 console.log(aImg)

2.也可以给创建的元素添加属性：
aImg.src = '../'  ----添加哪一张的图片
aImg.className = 'yi' ---起class名
aImg.style.border = '1px solid red'

3.追加元素对象：将创建好的元素追加到某个元素内部的后面
父元素.appendChild(创建的子元素)
var a = document.querySelector(".box");
 document.body.a.appendChild(cImg)---将创建好的img元素追加到body内部的最下面

4.插入元素对象：将创建好的元素追加到某个元素内部的前面
父元素.insertBefore(父元素)
var box = document.querySelector('.box')--必须先获取父元素
 document.body.insertBefore(cImg，box)---将创建好的img元素放前面，获取的父元素变量放后面

5.删除子元素：removeChild  ---将创建好的元素删除
var box = document.querySelector('.box')--必须先获取父元素
 document.body.removeChild(box)---删除父元素内部的所有子元素

# 如：删除父元素内的某一个子元素
  <body>
    <div class='box'>
      <img src="../img/女好骚.png" alt="" />
      <span>距离下线时间只剩100秒</span>
    </div>
  </body>
</html>
<script>
var a = document.querySelector(".box");   1.先获取父元素
var b = document.querySelector("span");   2.再获取父元素内的所有子元素
document.body.a.removeChild(b)
console.log(a)
</script>

# 如：删除父元素内的相同的某一个子元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
var a = document.querySelector('ul')         1.先获取父元素
var b = document.querySelectorAll('ul li')   2.再获取父元素内的所有子元素
for (i=0;i<b.length;i++){                    3.利用循环遍历所有的子元素
  b[i].onclick = function(){                 4.点击子元素的内容时
    a.removeChild(this)                      5.父元素（this指向谁时，删除谁）
  }
}
</script>

# 如：复制或克隆元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
  var a = document.querySelector("ul");  1.先获取要复制的元素
  var b = a.cloneNode()                  2.如果只要复制这个元素本身的话，（）内不加内容
  var b = a.cloneNode(true)              3.如果要复制这个元素本身以及内部的所有元素，（）内加true或非0的数字
  document.body.appendChild(b)           4.追加到body（父元素）内的最后面----如果父元素不是body，则要先获取父元素
</script>

# 如：替换元素
      ---父元素.replaceChild（添加的元素，被替换的元素）
      将ul元素替换成p元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
  var b = document.createElement("p");                    1.先创建一个p元素
  var a = document.querySelector("ul");                   2.获取被替换的ul元素
  b.style='width:20px;height:20px;border:1px red solid'   3.设置创建的p元素的css属性
  document.body.replaceChild(b,a)                         4.父元素.replaceChild（创建的元素，被替换的元素）
</script>                                                    ----如果父元素是自己设置的，则var获取父元素        

# 如 如果只想替换元素，而内容不变则
      ---父元素.replaceChild（添加的元素，被替换的元素）
      将ul元素替换成p元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
  var b = document.createElement("p");             1.先创建一个p元素
  var a = document.querySelector("ul");            2.获取被替换的ul元素
  b.innerHTML=a.innerHTML                          3.将p内的内容替换成ul的内容
  document.body.replaceChild(b,a)                  4.父元素.replaceChild（创建的元素，被替换的元素）
</script>  




