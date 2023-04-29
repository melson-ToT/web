# 一：事件对象的概述
1.在触发DOM上的某个事件时，会产生一个事件对象event,这个对象包含着所有事件相关的信息

2.标准浏览器的事件对象是时间处理函数中的第一个参数，可以通过参数获取对象
document.onclick=function(a){  //a:事件对象    MouseEvent鼠标
  console.log(a)       
}

3.注意：获取事件对象采用一种兼容写法，所有浏览器达成一致
document.onclick=function(ev){ 
  var ev = ev || event       
}

# 二.常见的事件类型：
1. 常用的鼠标事件

# 手机滑动事件：touch
# onload：xhr页面的内容（结构，数据）加载完毕，触发事件
# onreadystatechange：状态码发生改变，立刻触发此事件
# onhashchange:地址栏发生改变时
# onsubmit:表单提交事件，form发起的
# oninput:input的内容发生改变时触发
# onfocus:鼠标获得焦点
# onblur:鼠标失去焦点
# onclick：单击鼠标左键触发
# oncontextmenu:单击鼠标右键触发
ondblclick：双击鼠标左键触发
# onmousedown：鼠标按钮按下时触发（一般用于拖拽元素）---左右键和滚轮都可以触发
onmouseout：鼠标移出元素时触发
### onmousemove：鼠标移动时触发
# onmouseup：松开鼠标按键时触发（一般用于拖拽元素结束时）
onmouseover：鼠标移到元素上时触发
# onmouseleave：鼠标移出元素时触发（hover效果）
# onmouseenter：鼠标移入元素时触发（hover效果）

2. 常用的键盘事件

# onkeydown：按下按键时触发
# onkeyup：松开按键时触发
onkeypress：按下按键并产生字符时触发，忽略shift等功能键
# onkeyCode：返回keydown、keyup、keypress事件触发的键值的字符代码，或键的代码
oncharCode：返keypress事件触发的键值的ASCII码

3. HTML事件

# onload：页面完全加载后在window对象上触发
# unload：页面完全卸载后在window对象上触发
# select：选择了文本框的一个或多个字符时触发
# change：文本框失去焦点时，并且在它获取焦点后内容发生过改变时触发
# submit：单击“提交”按钮时在表单上触发
# focus：获得焦点时触发(不支持冒泡)
foucsin：获得焦点时触发（支持冒泡）
# blur：鼠标离开焦点时触发（input）或（textarea）
# resize：窗口大小发生变化时触发
foucsout：失去焦点时触发
# scroll：拖动滚动条时触发
textInput：可以用event.data获取当时输入的单个字符内容


# 三.event对象的属性介绍：
     一.event属性介绍
     1.type属性
     获取当前操作的事件类型,获取的事件类型不显示on
     document.onclick = function(e) {
         var e = e || window.event;
         alert(e.type); //click
     };
 
     2.button属性
     标准浏览器的鼠标事件，会有一个button属性，它是一个数字，代表鼠标按键。
     0代表鼠标按下了左键  1代表按下了滚轮    2代表按下了右键
     document.onmousedown = function(ev) {
         var ev = ev || window.event;
         alert(ev.button);
     };
 
     3.位置属性
     3.1.clientX,clientY：鼠标相对于可视区的位置。
     var pic = document.querySelector('img');
     document.onmousemove = function(e) {
         var e = e || event;
          console.log(e.clientX, e.clientY);
         pic.style.left = e.clientX - pic.offsetWidth / 2 + 'px'; //注意单位
         pic.style.top = e.clientY - pic.offsetHeight / 2 + 'px'; //注意单位
     }
 
     3.2.pageX,pageY：鼠标相对于文档的位置。
     document.onmousemove = function(e) {
         var e = e || event;
         console.log(e.clientX, e.clientY); //可视区
         console.log(e.pageX, e.pageY); //文档
     }
 
 
#     3.3.offsetX,Y:鼠标相对于操作元素(鼠标位置)到元素边缘(左上)的位置.
#       核心：和当前操作的元素有关----拖拽效果
     var pic = document.querySelector('img');
     pic.onmousemove = function(e) {
         var e = e || event;
         console.log(e.offsetX, e.offsetY);
     }
 
 
     3.4.screenX,screenY :鼠标相对于屏幕的位置。
     document.onmousemove = function(e) {
         var e = e || event;
         console.log(e.screenX, e.screenY);
     };
 
 
     4.键盘事件的属性
#    键盘事件添加给谁???    document
#    4.1.keyCode和which 获取键盘上按键对应的unicode编码
     数字0->48
     大写字母A->65
     小写字母a->97
     回车：13
     空格：32
 
###  event.ctrlKey、event.altKey、event.shiftKey 分别代表ctrl alt shift键
     document.onkeydown = function(e) { //键盘按下
         var e = e || event;
         console.log(e.keyCode);
         console.log(e.which);
     };
 
 
### 不用按钮，用键盘来代替回车键，发送消息    ctrl+enter表示
    document.onkeydown = function(e) { //键盘按下
         var e = e || event;
#         if (e.ctrlKey && e.keyCode === 13) { 表示Ctrl和Enter一起按
             console.log(123);
         }
     };
 
 
     阻止复制
     document.onkeydown = function(e) { //键盘按下
         var e = e || event;
         if (e.ctrlKey || e.keyCode === 123) {
             alert('你乱按什么啊');
             return false;
         }
     };
 
     document.oncontextmenu = function() {
         alert('你乱按什么啊,右键也不行');
         return false; //阻止浏览器的默认行为
     };
    var arr = [1, 2, 3, 4, 5, 6, 7];
     var arrStr = ["a ", "v", "b", "d"];
     console.log(arr.push(8, 9));
     console.log(arr.sort(function compar(a, b) {
         b - a
     }));
    console.log(arr.join("a"));
     console.log(arrStr);
    console.log(arr);

# 四.取消浏览器默认的行为：ventDdfault
1.ev.preventDdfault():标准浏览器取消默认行为
2.ev.returnValue=false;非标准浏览器取消默认行为
3.return false:普通处理函数
# 就会取消a标签的跳转
    <a href="">百度</a>
  </body>
</html>
<script>
  var oA = document.querySelector("a");
  oA.onclick = function (ev) {
    ev = ev || window.event;  //兼容浏览器
    ev.returnValue = false;   //取消浏览器默认的行为
  };

# 取消右键点击行为(1、2都可以)
 1. document.oncontextmenu = function () { 
    return false;
  };

 2. document.oncontextmenu = function (ev) {
    ev = ev || window.event;
    ev.returnValue = false;
  };


# 案例1：右键点击空白区域，盒子出现在鼠标位置，左键点击消失
  <style>
    .box {
      width: 200px;
      height: 400px;
      background-color: red;
      display: none;              1.给盒子设一个没有
      position: absolute;         2.给定位
    }
  </style>
  <body>
    <div class="box"></div>
  </body>
</html>
<script>
   var oBox = document.querySelector(".box");   1.取到元素
  document.oncontextmenu = function (ev) {      2.右键点击document，不能点击元素
     ev = ev || window.event;                   3.兼容浏览器
     ev.returnValue = false;                    4.取消右键的默认行为
     oBox.style.display='block'                 5.点击右键时，盒子出现
     oBox.style.left=ev.clientX+'px'            6.盒子的left定位等于鼠标在可视区域横轴的位置
     oBox.style.top=ev.clientY+'px'             7.盒子的top定位等于鼠标在可视区域纵轴的位置
   };
document.onclick=function(){                    8.左键点击document
  oBox.style.display='none'                     9.盒子消失
}
</script>

# 时间流--的时间冒泡
1.事件流指：接收事件的顺序：标签-body-HTML-document
2.事件流包括三个阶段：
                   1.事件捕捉阶段
                   2.目标阶段
                   3.事件冒泡阶段
# 3.事件冒泡：
            --事件开始时，从具体的元素开始接收，然后逐级向上传播直到-document