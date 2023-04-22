# 一.事件委托：
           ----利用冒泡机制，将子元素的事件委托给父元素执行
           ----获取当前操作元素目标元素：ev.target || ev.srcElement

      1.target  获取父元素中的子元素  
      2.type    获取事件类型
      3.target.nodeName  父元素中子元素的标签名称
      4.target.tagName  父元素中子元素的节点名称

# 事件委托的注意点：
1.如果无法获取元素，只能获取元素的父元素target
2.如果子元素太多，可以考虑循环或事件委托
3.如果没有事件，就没有事件委托

# 案例1：点击li时，出现背景颜色，点击下一个li上一个的背景颜色消失，点击空白，li的背景颜色都消失
  <style></style>
  <body>
    <ul>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
    </ul>
  </body>
</html>     1.第一次为false冒泡，点击对应的li时，阻止上传  2.点击document空白为true，变为事件绑定，会逐级向下传播。相当于点击document时，也点击了li，所以点击下一个li时，上一个li会消失
<script>      
  var ul = document.querySelector("ul");
  var li = document.querySelectorAll("ul li");
  for (var i = 0; i < li.length; i++) {           1.循环所有li的的索引
    function fn() {
      this.style.backgroundColor = "red";         3.谁调用我，this指向谁（li）颜色为：
    }
    li[i].addEventListener("click", fn, false);2.第一次为false冒泡，点击对应的li时，li改变颜色
    }
    function jon() {
      for (var j = 0; j < li.length; j++) {       5.由于true事件监听自上而下扩展，document会影响到li[j]，所以点击下一个li时，上一个li的颜色消失
        li[j].style.backgroundColor = null;
      }
    }
    document.addEventListener("click", jon, true); 4.点击空白时，true事件监听             
</script>

#  或：
  var ul = document.querySelector("ul");
  var li = document.querySelectorAll("ul li");
  for (i=0;i<li.length;i++){
    function fn (){
      this.style.backgroundColor = 'red'
    }
    li[i].addEventListener('click',fn,false)
  }
  function obj(){
    for (j=0;j<li.length;j++){
      li[j].style.backgroundColor = null
    }
  }
  document.addEventListener('click',obj,true)
</script>

# 二.事件委托：
           1.没有循环，给ul元素添加点击事件
           2.下面的方式减少事件绑定的绑定次数

# 案例2.  用ev.target 方法获取父元素中的子元素
  <body>
    <ul>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
    </ul>
  </body>
</html>
<script>
  var ul = document.querySelector("ul"); 
  ul.onclick = function (ev){
    var ev = ev || event
    if(ev.target.nodeName === 'LI'){            ul.子元素.标签名称 === 显示的LI时   
      ev.target.style.display = 'none'          ul.子元素.消失
    }
  }
</script>


# 案例3.  获取数组的value值，添加给父元素中的子元素中区，再用ev.target删除子元素，
<script>  forEach循环，不能写为str='<li>' + value + '</li>'，不然显示的只有最后的8888
  var ul = document.querySelector("ul"); 
  var arr = [1111,2222,3333,4444,5555,6666,7777,8888]
  var str = ''                     str将输入值转换为其相应的字符串形式
  arr.forEach(function(value){     forEach循环，循环value值
    str+='<li>' + value + '</li>'  转换为字符串=value值加第一个value值
  }) 
  ul.innerHTML = str               ul的内容=所有循环的str
  ul.onclick = function(ev){       点击父元素内的（ev.target父元素内的）
    ev = ev || event
    ev.target.style.display = 'none'  父元素相应的子元素消失
  }
</script>
