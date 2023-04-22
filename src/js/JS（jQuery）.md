# 一：jQuery的地址
1. https://www.lanrenzhijia.com/
2. https://www.jq22.com/
3. 本地引入jQuery：jQuery cdn



# 二.Jquery的核心语法：
1. $符号：
      jQuery源码中的一句代码：window.jQuery = window = jQuery
      jQuery内库的核心对象叫做：jQuery ，给jQuery取一个别名叫做jQuery

      $('.box') = jQuery('.box')

2. window.onload = function(){} 和 $(document).ready(function(){}) 的区别
  （1）window.onload通过此事件将js代码写入文档的任意位置
  （2）window.onload表示页面的内容（结构、页面的数据）加载完成后触发
  （3）$(document).ready（）表示页面的结构加载后触发，但是比window.onload要快
  （4）window.onload一个页面是能存在一个，多个会被覆盖
  （5）$(document).ready（）一个页面可以存在多个，按照顺序触发
  （6）$(document).ready（）简写：$()
   (7)window.onload没有简写

3. $(document).ready（）简写：$()  的案例：
<body>
    <div class="box">我是box的内容</div>
  </body>
  (原生js)<script>
    window.onload = function(){
      console.log(document.querySelector('.box').innerHTML);
    }
  </script>
  
  (jQuery内库)<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
  <script>
    $(function(){
      console.log($('.box').html());
    })
  </script>

4. jQuery类库的方法分为两类
（1）实例方法：jQuery类下面的，只能是jQuery对象（通过jQuery获取的元素）使用，原生js不能使用
（2）工具方法：前面带有$.开头的，工具方法原生js和jQuery对象都能使用

5. jQuery里面都是方法，采用链式调用
问题：如何实现方法的链式调用，每个方法内部返回一个this(return this)
案例：
    $('button').click(function(){
        $(this).addClass('active').siblings('button').removeClass('active');
        $(.item).er($(this).index()).show().siblings('tab'.item).hide()
    })

6. 原生的js对象和jQuery对象可以相互转换
  <script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
  <script>
    let p = document.querySelector('.box') //原生js
    console.log(p);
    打印的结果：<div class="box">我是box的内容</div>
    
    let p1 = $('.box') //jQuery
    打印的结果：html:20 n.fn.init [div.box, prevObject: n.fn.init(1), context: document, selector: ".box"]
  </script>

7. 原生js对象如何转换成jQuery对象，通过索引方式或者jQuery下面的get方法

   console.log(p)  =>     console.log($(p))

8. jQuery对象如何转换成原生js对象，将对象名称放到$()内即可

   console.log(p1)  =>   console.log(p1[0]);
   这里的索引，就是选择第一个获取的对象

9. jQuery是无法直接使用.innerHTML

   （1）可以先转为原生方法：索引
                   console.log(p1[0].innerHTML)

   （2）可以先转为原生方法：get
                   console.log(p1.get(0).innerHTML)


# 三.jQuery的方法介绍：
$(this).hide() - 隐藏当前元素

$("p").hide() - 隐藏所有段落

$(".test").hide() - 隐藏所有 class="test" 的所有元素

$("#test").hide() - 隐藏所有 id="test" 的元素


语法	描述
$(this)	当前 HTML 元素
$("p")	所有 <p> 元素
$("p.intro")	所有 class="intro" 的 <p> 元素
$(".intro")	所有 class="intro" 的元素
$("#intro")	id="intro" 的元素
$("ul li:first")	每个 <ul> 的第一个 <li> 元素
$("[href$='.jpg']")	所有带有以 ".jpg" 结尾的属性值的 href 属性
$("div#intro .head")	id="intro" 的 <div> 元素中的所有 class="head" 的元素


jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性。
$("p").css("background-color","red");



jQuery 事件函数
jQuery 事件处理方法是 jQuery 中的核心函数。

事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。术语由事件“触发”（或“激发”）经常会被使用。

通常会把 jQuery 代码放到 <head>部分的事件处理方法中：

实例
<html>
<head>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $("button").click(function(){
    $("p").hide();
  });
});
</script>
</head>



# 四.jQuery的方法
1. 获取元素：
   单个元素：$('li')
   多个元素：$('ul li')

2. eq(index|-index):获取第N个元素，里面的索引编号从0开始
   正数从0开始：$('ul li').eq(0)  //获取第一个li元素
   负数从-1开始

3. find():找出这个元素的子元素
   console.log($('ul').find('li').find('a'));）
   获取 ul 里面的 li 里面的 a

4. on():事件处理函数
        on(events,[selector],[data],fn):
        参1：events 事件的类型，可以添加多个事件，空格分开，比如：click mouseover
        参2：[selector] 事件委托的选择器，没有可以不写
        参3：[data] 事件可以传递数据，没有可以不写
        参4：fn，事件处理的函数

5. addClass()和removeClass(),添加/删除对应的class，()内没有.
         $('li').addClass('li2'),给这个li加一个class名为li2，不加(.li2)点
         $('li').removeClass('li2'),给这个li删除class名为li1，不加(.li2)点

6. siblings(li):获取这个元素的兄弟元素（除了自身元素）
             1.siblings()内可以不带元素，但是防止兄弟元素中，还有其他的元素，比如：选择li里，让这些li标签做选项卡效果，但是ul内不止li标签，还有p标签，那么我们就在siblings()内加li，表示，是有和这些li有关的，


7. 用jQuery：Tab选项卡效果：
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
    const $ali = $('ul li')
    const $oli = $('ol li')
   $ali.on('mouseenter',function(){
      $(this).addClass('active').siblings('li').removeClass('active')
      当前元素.  添加（class名）.兄弟元素（li）.删除（class名）
      $oli.eq($(this).index()).show().siblings('li').hide()
      当前元素对应(ul li 的索引).出现  .兄弟元素.消失
   })
  </script>


8. show()，hide()
   show()元素出现
   show(300)300ms内有慢慢出现
   hide()元素隐藏
   hide(300)300ms内有慢慢消失


9. index()获取对应的索引值，从0开始
   $(this).index():获取当前li的索引

10. html():相当于js的innerHTML

11. text():相当于js的innerText，元素文本内容

12. val():相当于js的value，元素表单内容值

13. first():获取第一个元素，$('li').eq(0)

14. list():获取最后一个元素，$('li').eq($('li').length-1)

15. $('li').first().nextAll()：第一个li元素之后的所有元素


# 五.商城的楼梯效果：
1. offset():相当于原生js的offsetLeft/offsetTop
   console.log($('ul').eq(0).offset().top)
                获取ul.第一个索引.top
      console.log($('ul').eq(0).offset().left)
                获取ul.第一个li.left

2. each()遍历循环：对每个li元素进行遍历
      $('li').each(index,$(element)){
        console.log(index)     //0-9
        console.log($(element))//元素本身
      }

3. scrollTop(),获取元素相对于滚动条距离顶部的偏移
   $(window).on('scroll',function){
    console.log($(window).scrollTop(1000px))
   }

4. 宽/高的计算方法：
width()         内容的宽度
heigth()        内容的高度
innerWidth()    内容+padding的宽度
innerHeiht()    内容+padding的高度
outerWidth()    内容+padding+border的宽度
outerHeiht()    内容+padding+border的高度
outerWidth(true)    内容+padding+border+margin的宽度

5. 动画效果：animate()
   对象做参数，改变的物体的属性集合
   如果需要改变物体的背景颜色，添加jQuery.color,js插件
<style>
  .box {
    width: 200px;
    height: 200px;
    background-color: red;
    position: absolute;      1.所有的物体运动，都要绝对定位
  }
  </style>
  <body>
   <div class="box"></div>
  </body>
  </html>
  <script src="https://code.jquery.com/jquery-3.0.0.min.js"></script>
  <script>
    $('.box').on('click',function(){  2.点击box事件处理
      $('.box').animate({             3.box.动画(向右移动600px，3000毫秒的时间)
        left : 600
      },3000).animate({               4.box.动画(透明度变成0，3000毫秒的时间)
        opacity:0
      },3000).animate({               5.box.动画(透明度变成1，3000毫秒的时间)
        opacity:1
      })
    })
  </script>


# 六.轮播图的jQuery幻灯片效果
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <style>
    *{
      margin: 0;
      padding: 0;
      }
    .father {
      width: 400px;
      height: 400px;
      border: 1px black solid;
      box-sizing: border-box;
      margin: 100px auto 0;
      position: relative;
      overflow: hidden;
    }
    ul {
      display: flex;
      padding: 0;
      position: absolute;
    }
    ul li{
      flex-shrink: 0;
      list-style: none;
    }
    ul li img{
      width: 400px;
      height: 400px;
    }
    ol {
      list-style: none;
      position: absolute;
      top: 370px;
      left: 95px;
    }
    ol li{
      list-style: none;
      float: left;
      width: 20px;
      height: 20px;
      background-color: blue;
      border-radius: 10px;
      margin-right: 5px;
    }
    ol li.ccc {
      background-color: red;
    }
    .left{
      position: absolute;
      top: 100px;
      left: 20px;
      font-size: 100px;
      color: burlywood;
    }
    .right{
      position: absolute;
      top: 100px;
      right: 20px;
      font-size: 100px;
      color: burlywood;
    }
    </style>
     <body>
        <div class="father">
          <ul>
            <li><img src="../img/img222/1.png" alt=""></li>
            <li><img src="../img/img222/2.png" alt=""></li>
            <li><img src="../img/img222/3.png" alt=""></li>
            <li><img src="../img/img222/4.png" alt=""></li>
            <li><img src="../img/img222/5.png" alt=""></li>
            <li><img src="../img/img222/6.png" alt=""></li>
            <li><img src="../img/img222/7.png" alt=""></li>
            <li><img src="../img/img222/8.png" alt=""></li>
            <li><img src="../img/img222/9.png" alt=""></li>
            <li><img src="../img/img222/1.png" alt=""></li>
          </ul>
          <ol>
            <li class="ccc"></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
          </ol>
          <span class="left"><</span>
          <span class="right">></span></span>
     </body>
     </html>
     </html>
  <script src="https://code.jquery.com/jquery-3.0.0.min.js"></script>
  <script>
    !function ($){
      const $father = $('.father')
      const $ul = $('ul')
      const $ulli = $('ul li')
      const $ol = $('ol')
      const $olli = $('ol li')
      const $left = $('.left')
      const $right = $('.right')
      let $num = 0                           1.先给$num赋值
      const $liwidth = $ulli.eq(0).width()   2.li的宽度=第一个li的宽度
      $ul.width($liwidth * $ulli.length)     3.ul的宽度=li的宽度*长度）   
      $olli.on('mouseenter',function(){      4.鼠标移入小球时
        $num = $(this).index()               5.$num=小球的索引
        $olli.eq($num).addClass('ccc').siblings('li').removeClass('ccc')
        6.当前小球的索引，加Class名，变颜色，兄弟的li，删除Class名

        $ul.animate({     7.ul.动画
          left:-$liwidth * $num  8.横向：负的.li的宽度*小球的索引
        })
      })
      $right.on('click',function(){  9.点击右键
        $num++                         
        if($num === $olli.length){   10.如果小球的索引=第10张图片（没有第10张图片）
          $ul.css('left',0)          11.ul的left回到0的位置
          $num = 0                   12.小球的索引=0
        }
        $olli.eq($num).addClass('ccc').siblings('li').removeClass('ccc')
          $ul.animate({
            left:-$liwidth * $num
          })
      })
      $left.on('click',function(){   13.点击左键键
        $num--                       
        if($num <= -1){              14.如果小球的索引=-1（没有-1）
          $ul.css('left',-$liwidth * $olli.length-1)
            15.ul的left回到最后一张图片的位置
          $num = $olli.length-1      16.小球的索引=最后一个
        }
        $olli.eq($num).addClass('ccc').siblings('li').removeClass('ccc')
          $ul.animate({
            left:-$liwidth * $num
          })
      })
    }(jQuery)
  </script>

















































5. 用jQuery的事件委托做：Tab选项卡效果：
  <body>
    <ul>
      <li>
        <a href="#" style="color: red">ww</a>
      </li>
      <li>
        <a href="#">ww</a>
      </li>
      <li>
        <a href="#">ww</a>
      </li>
      <li>
        <a href="#">ww</a>
      </li>
    </ul>
  </body>
  </html>
  <script src="https://code.jquery.com/jquery-3.0.0.min.js"></script>
  <script>
   $('ul').on('mouseover','ul li a',function(){
      $(this).css('color','red')
   })
  </script>


