# 一.拖拽效果：
1.拖拽所需的事件类型：
                  onmousedown：鼠标按钮按下时触发
                  --确定鼠标距离盒子的左上角位置不变

                  onmousemove：鼠标移动时触发--鼠标移动时，有一个不断变化的鼠标位置
                  --鼠标位置-减去-盒子左上角的位置

                  onmouseup：松开鼠标按键时触发
                  --结束鼠标移动事件

###  拖拽案例：1
      2.拖拽的元素一定具有定位属性：position:absolute；改变元素的位置
<script>
  var div = document.querySelector("div");
  div.onmousedown = function (ev) {             1.鼠标按下div时
    var ev = ev || event;                       2.当前事件函数
    var x = ev.offsetX;                         3.变量x = 获取当前div在页面中向右位置
    var y = ev.offsetY;                         4.变量y = 获取当前div在页面中向下位置
    document.onmousemove = function (ev) {      5.鼠标移动到空白区域时
      var ev = ev || event;                     6.当前事件函数
      div.style.left = ev.clientX - x + "px";   7.此时div横向位置 = 当前鼠标在页面横向位置 - 之前div在页面中向右位置
      div.style.top = ev.clientY - y + "px";    8.此时div纵向位置 = 当前鼠标在页面纵向位置 - 之前div在页面中向下位置
    };
    document.onmouseup = function () {          9.鼠标松开空白处时，
      document.onmousemove = null;              10.结束鼠标不移动的事件
      document.onmouseup = null;                11.结束鼠标松开的事件----影响内存
    };
    ev.returnValue=false                   注意：12.如果是图片，则浏览器的默认行为不允许拖拽行为，此时需要加ev.returnValue=false：取消浏览器的默认行为
  };
</script>

### 拖拽案例2：---因为div初始的位置不变，所以鼠标按下、移动时，每次都是针对div第一次的位置，进行变化的
<script>
  var div = document.querySelector("div");
  div.onmousedown = function () {
    document.onmousemove = function (ev) {
      var ev = ev || event;
      div.style.left = ev.clientX + "px";
      div.style.top = ev.clientY + "px";
    };
    document.onmouseup = function () {
      document.onmousemove = null;
      document.onmouseup = null;
    };
  };
</script>

### 拖拽案例3：---让图片不能超出页面的可视范围：
<script>
  var img = document.querySelector("img");
  img.onmousedown = function (ev) {
    var ev = ev || event;
    var x = ev.offsetX;                          1.当前图片在页面的left距离
    var y = ev.offsetY;                          2.当前图片在页面的top距离
    document.onmousemove = function (ev) {
      var ev = ev || event;
      var xx = ev.clientX - x                    3.xx=此时鼠标移动的left距离
      var yy = ev.clientY - y                    4.xx=此时鼠标移动的top距离
      if(xx<0){    5.如果鼠标移动的左边距离超出页面
        xx=0       6.鼠标距离左边的距离为0px

      }else if(xx >  - img.offsetWidth){
        xx = document.documentElement.clientWidth - img.offsetWidth
      }    7.如果鼠标移动的右边距离超出页面，鼠标距离右边的距离为0px

      if(yy<0){   8.如果鼠标移动的上边距离超出页面
        yy=0      9.鼠标距离上边的距离为0px
      }else if(yy > document.documentElement.clientHeight - img.offsetHeight){
        yy = dodocument.documentElement.clientWidthcument.documentElement.clientHeight - img.offsetHeight
      }   10.如果鼠标移动的下边距离超出页面，鼠标距离下边的距离为0px

      img.style.left = xx + "px";
      img.style.top = yy + "px";
    };
    document.onmouseup = function () {
      document.onmousemove = null;
      document.onmouseup = null;
    };
    ev.returnValue = false;
  };
</script>

### 拖拽案例3：---让图片不能超出父元素的范围：
  <style>
    div {
      width: 800px;
      height: 400px;
      border: 2px red solid;
      position: relative;
      margin: 100px auto;
    }
    img {
      width: 100px;
      position: absolute;
    }
  </style>
  <body>
    <div><img src="../img/女好骚.png" alt="" /></div>
  </body>
</html>
<script>
  var img = document.querySelector("img");
  var div = document.querySelector('div')
  img.onmousedown = function (ev) {
    var ev = ev || event;
    var x = ev.offsetX;
    var y = ev.offsetY;
    document.onmousemove = function (ev) {
      var ev = ev || event;
      var xx = ev.clientX - x - div.offsetLeft
      var yy = ev.clientY - y - div.offsetTop
      if(xx<0){
        xx=0
      }else if(xx > div.offsetWidth - img.offsetWidth){
        xx = div.offsetWidth - img.offsetWidth
      }
      if(yy<0){
        yy=0
      }else if(yy > div.offsetHeight - img.offsetHeight){
        yy = div.offsetHeight - img.offsetHeight
      }
      img.style.left = xx + "px";
      img.style.top = yy + "px";
    };
    document.onmouseup = function () {
      document.onmousemove = null;
      document.onmouseup = null;
    };
    ev.returnValue = false;
  };
</script>
