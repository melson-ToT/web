# 一.时间流--的时间冒泡
1.事件流指：接收事件的顺序：标签-body-HTML-document
2.事件流包括三个阶段：
                   1.事件捕捉阶段
                   2.目标阶段
                   3.事件冒泡阶段
# 3.事件冒泡：
            --事件开始时，从具体的元素开始接收，然后逐级向上传播直到-document
  
#  案例1：
1.点击button按钮时，.box出现
2.点击document空白时，.box消失
#   3.注意：此时点击button时，什么都不会出现，因为浏览器同时识别，你点击了button和document空白，因为， 点击button也是document内的，是因为冒泡事件带来的负面影响
 <style>
    .box {
      width: 200px;
      height: 400px;
      background-color: red;
      display: none;
    }
  </style>
  <body>
    <button>显示</button>
    <div class="box"></div>
  </body>
</html>
<script>
  var oBox = document.querySelector(".box");
  var button = document.querySelector("button");
  button.onclick = function (ev) {
    ev = ev || window.event;
    oBox.style.display = "block";
    ev.stopPropagation()    ------阻止目标元素不要往上传递
  };
document.onclick=function(){
  oBox.style.display = "none";
}
</script>

# 二.阻止冒泡：
         ----阻止冒泡的核心：阻止目标元素不要往上传递
         ----取消冒泡：让当前操作的元素（冒泡元素），不会冒泡到父元素

1. 标准浏览器取消冒泡：ev.stopPropagation()
2. IE浏览器取消冒泡：ev.cancelBubble=true

# 案例2:点击盒子，模拟的下拉菜单出现，点击空白下拉菜单消失，点击某个下拉菜单，会显示在盒子上，同时下拉菜单消失
    .box {
      width: 84px;
      height: 20px;
      background-color: red;
      padding: 0 10px;
      line-height: 20px;
      text-align: center;
      margin: 50px auto;
    }
    ul {
      position: absolute;
      top: 54px;
      left: 371px;
      padding: 0;
      line-height: 80px;
      display: none;
    }
    li {
      width: 100px;
      height: 20px;
      list-style: none;
      line-height: 20px;
      text-align: center;
      background-color: blue;
      border: 2px brown solid;
      border-bottom: 0;
    }
    li:nth-child(4) {
      border-bottom: 2px;
    }
  </style>
  <body>
    <div class="box">请选择内容</div>
    <ul>
      <li>魔兽世界</li>
      <li>QQ炫舞</li>
      <li>英雄联盟</li>
      <li>地下勇士</li>
    </ul>
  </body>
</html>
<script>
  var ul=document.querySelector('ul')
  var box = document.querySelector(".box");
  var li = document.querySelectorAll("ul li");
  box.onclick=function(ev){                     1.点击box
    var ev = ev || window.event                     2.浏览器兼容
    ul.style.display='block'                    3.ul消失
    ev.stopPropagation()                        4.阻止这个点击事件向上冒泡
  }
  document.onclick=function(){                  5.点击空白
    ul.style.display='none'                     6.lu消失
  }
  for (i=0;i<li.length;i++){                    7.循环li的索引
    li[i].onclick=function(ev){                 8.点击li的索引值（内容）
      box.innerHTML=this.innerHTML              9.box的内容=li的索引值（内容）
      ul.style.display='none'                   10.ul消失
      ev.stopPropagation()                      11.阻止这个点击事件向上冒泡
    }
  }

##### 注意：利用冒泡的优点
  for (i=0;i<li.length;i++){                    7.循环li的索引
    li[i].onclick=function(ev){                 8.点击li的索引值（内容）
      box.innerHTML=this.innerHTML              9.box的内容=li的索引值（内容）
      ul.style.display='none'  // 这两行可以不用写：因为:上面已经有一个 document的点击事件了，同时有两个点击事件的话，则以document为准，刚好利用了冒泡的优点，让ul消失  
      ev.stopPropagation()     //                 
    }
  }

# 案例3.跟随鼠标的提示框：
<body>
    <ul>
      <li><a href="" xs='无无无无无无无无无无无无无无无无无'>新闻</a></li>
      <li><a href="" xs='拜拜白白不不不不不不不不不不不不不不'>军事</a></li>
      <li><a href="" xs='谢谢谢谢谢寻寻寻寻寻寻寻寻'>体育</a></li>
      <li><a href="" xs='坎坎坷坷扩扩扩扩扩扩扩'>教育</a></li>
    </ul>
    <div>你出来</div>
  </body>
</html>
<script>
    var a = document.querySelectorAll("ul li a");
    var div = document.querySelector("div");
    for (i=0;i<a.length;i++){
      a[i].onmouseenter = function(ev){
        var ev = ev || event
        div.innerHTML=this.innerHTML //1.鼠标移入什么，就显示a[i]的内
        div.innerHTML=this.getAttribute('xs')//2.鼠标移入什么，就显示自定义属性的内容
        div.style.display = 'block'
        div.style.left = ev.clientX+'px'
        div.style.top = ev.clientY+'px'
      }
      a[i].onmouseleave = function(){
        div.style.display = 'none'
      }
    }

# 案例4.(如果是：一个标签对应一个一个标签)跟随鼠标的提示框：
    var oa = document.querySelectorAll('.ol li');
    var li = document.querySelectorAll('.ul li');
      oa.forEach((item, i)=> {
        oa[i].onmouseover = function(ev) {      1.鼠标移入对应的a标签时
          li[i].style.display = 'block';        2.对应的li标签的索引值出现
          li[i].style.left = i * 300 + 'px'     3.对应的li标签的位置为索引*300px
        }
        oa[i].onmouseout = function() {         4.鼠标移开时，
          li[i].style.display = 'none';         5.对应的li标签的索引值消失
        }
      })

      var obj = {                   1.对象
        a: 2,
        b: 2,
      }
      for (var i in obj) {          2.for in 循环，循环它的属性名称，和属性值
        // a  obj.a
      } 
      var arr = [3,4,5]             3.for of循环，循环它的索引值，不要索引
      for (var value of arr) {
        3,4,5
      }                             