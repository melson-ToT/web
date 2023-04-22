# 一：匀速运动的原理：
1. 运动--改变盒子的CSS属性
2. 通过定时器不断的改变CSS属性
3. 问题：频繁的点击盒子，定时器会叠加，盒子的速度越来越快
4. 结局的方式：每次开启一个定时器，关闭之前的定时器
<script>
const father = document.querySelector('.father')
let time = null                   1.先给定时器设为没有
father.onclick = function(){
  clearInterval(time)             2.每次点击之前关闭定时器
  time = setInterval(function(){  3.开启定时器
    father.style.left = father.offsetLeft + 5 +'px'
  },20)
}
</script>

# 二.缓冲运动的原理：
          ----由快到慢：
案例一：

  <style>
.box1 {
  width: 100px;
  height: 50px;
  background-color: blue;
  position: absolute;           1.给盒子一个绝对定位
  top: 0;
  left: 0;
}
</style>
 <body>
    <div class="box1"></div>
 </body>
 </html>
 </html>
 <script>
const box1 = document.querySelector('.box1')
let time = null                             2.给time一个返回值
box1.onclick = function(){
  clearInterval(time)                       3.先消除定时器
  time = setInterval(function(){
    deep = (700 - box1.offsetLeft) / 10     
    4.deep=（目的地 - 盒子的left位置）除以20，这样盒子每次运动时，都会比上一次运动的速度慢，除以后面的数，越大，速度就会越慢

    deep = deep > 0 ? Math.ceil(deep):Math.floor(deep)
    5.如果（目的地 - 盒子的left位置）除以20大于0，则向上取整，否则，向下取整（由于盒子的位置有可能在目的地的左右两侧，防止盒子的最终位置不到位）

    if(box1.offsetLeft === 700){
      clearInterval(time)
    6.盒子的left位置到达目的地，则消除定时器

    }else{
      box1.style.left = box1.offsetLeft + deep + 'px'
    7.如果盒子没有到达时，它的位置=不断获取运动的位置+缓冲的速度
    }
  },1000/60)
}
</script>

案例2，封装函数：
  <style>
.box1 {
  width: 100px;
  height: 50px;
  background-color: blue;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
 <body>
    <div class="box1"></div>
 </body>
 </html>
 </html>  ###注意：.后面不能直接加形参，可以[objvalue]或[value]
 <script>
const box1 = document.querySelector('.box1')
let time = null
function sss(obj,value){    1.封装函数，将变化的值，放入（）内
  clearInterval(time)
  time = setInterval(function(){
    deep = (value - obj.offsetLeft) / 10                2.此时value为形参
    deep = deep > 0 ? Math.ceil(deep):Math.floor(deep)
    if(obj.offsetLeft === value){  3.此时obj为形参
      clearInterval(time)
    }else{
      obj.style.left = obj.offsetLeft + deep + 'px'
    }
  },1000/60)
}
box1.onclick= function(){
  sss(this,700) 1.this为实参，指box1  ，700为实参
}
</script>


# 七.多属性运动（链式）与封装函数

  案例1.没有加封装函数的多属性运动
<style>
.box {
  width: 100px;
  height: 100px;
  background-color: red;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
 <body>
<div class="box"></div>
 </body>
 </html>
 </html>
 <script>
const box = document.querySelector('.box')
let time = null
box.onmouseenter = function(){
  clearInterval(time)
  time = setInterval(function(){
    beed = (800 - box.offsetWidth) / 20
    beed = beed>0? Math.ceil(beed):Math.floor(beed)
    if(box.offsetWidth === 800){
      clearInterval(time)
    }else{
      box.style.width =box.offsetWidth + beed +'px'
    }
  },1000 / 60)
}
box.onmouseleave = function(){
  clearInterval(time)
  time = setInterval(function(){
    beed = (100 - box.offsetWidth) / 20
    beed = beed>0? Math.ceil(beed):Math.floor(beed)
    if(box.offsetWidth === 100){
      clearInterval(time)
    }else{
      box.style.width =box.offsetWidth + beed +'px'
    }
  },1000 / 60)
}
</script>

案例2：进行封装函数的多属性运动：
 <script>
const box = document.querySelector('.box')
let time = null
function sss(obj,value){
  clearInterval(time)
  time = setInterval(function(){
    beed = (value - obj.offsetWidth) / 20
    beed = beed>0? Math.ceil(beed):Math.floor(beed)
    if(obj.offsetWidth === value){
      clearInterval(time)
    }else{
      obj.style.width =obj.offsetWidth + beed +'px'
    }
  },1000 / 60)
}
box.onmouseenter = function(){
  sss(this,800)
}
box.onmouseleave = function(){
  sss(this,100)
}
</script>

案例3：将属性进行封装函数的多属性运动：
# 模拟二级栏
<style>
.father {
  width: 200px;
  height: 50px;
  background-color: red;
  margin: 100px auto;
  position: relative;
}
.box {
  width: 200px;
  height: 0;
  background-color: blue;
  position: absolute;
  top: 50px;
  left: 0;
  overflow: hidden;        1.超出部分被隐藏
}
</style>
 <body>
  <div class="father">
    <div class="box">
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
    </div>
  </div>
 </body>
 </html>
 </html>
 <script>
  const father = document.querySelector('.father')
  const box = document.querySelector('.box')
  let time = null
  function sss(obj,value,att){
    clearInterval(time)
    time = setInterval(function(){
      let kuai = parseInt(window.getComputedStyle(obj)[att])
                2.取代 box.offsetHeight的方法
      beed = (value - kuai) / 20
      beed = beed>0? Math.ceil(beed):Math.floor(beed)
      if(kuai === value){
        clearInterval(time)
      }else{
        obj.style[att] =kuai + beed +'px'
      }
    },1000 / 60)
  }
  father.onmouseenter = function(){
    box.style.display='block'       3.点击时，出现
    sss(box,150,'height')
  }
  father.onmouseleave = function(){
    sss(box,0,'height')  
  }
  </script>

案例4：鼠标移入，目标缓冲出来
<style>
  .father {
    width: 200px;
    height: 50px;
    background-color: red;
    margin: 100px auto;
    position: relative;
  }
  .box {
    width: 200px;
    height: 0;
    background-color: blue;
    position: absolute;
    top: 50px;
    left: 0;
    overflow: hidden;
  }
</style>
<body>
  <div class="father">
    <div class="box">
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
    </div>
  </div>
</body>
</html>
</html>
<script>
  const father = document.querySelector('.father')
  const box = document.querySelector('.box')
  let time = null
  father.onmouseenter = function () {
    box.style.display = 'block'
    clearInterval(time)
    time = setInterval(function () {
      let Height = box.offsetHeight
      beed = (150 - Height) / 20
      beed = beed > 0 ? Math.ceil(beed) : Math.floor(beed)
      if (Height === 150) {
        clearInterval(time)
      } else {
        box.style.height = Height + beed + 'px'
      }
    }, 1000 / 60)
  }
  father.onmouseleave = function () {
    clearInterval(time)
    time = setInterval(function () {
      let Height = box.offsetHeight
      beed = (0 - Height) / 20
      beed = beed > 0 ? Math.ceil(beed) : Math.floor(beed)
      if (Height === 0) {
        clearInterval(time)
      } else {
        box.style.height = Height + beed + 'px'
      }
    }, 1000 / 60)
  }
</script>

案例5：鼠标移入，目标缓冲出来,面向对象的方法
<style>
  .father {
    width: 200px;
    height: 50px;
    background-color: red;
    margin: 100px auto;
    position: relative;
  }
  .box {
    width: 200px;
    height: 0;
    background-color: blue;
    position: absolute;
    top: 50px;
    left: 0;
    overflow: hidden;
  }
</style>
<body>
  <div class="father">
    <div class="box">
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
    </div>
  </div>
</body>
</html>
</html>
<script>
  function Fans(){
    this.father = document.querySelector('.father')
    this.box = document.querySelector('.box')
  }
  Fans.prototype.init = function(obj,value){
    let time = null
    clearInterval(time)
    time = setInterval(()=> {
      let Height = obj.offsetHeight
      beed = (value - Height) / 20
      beed = beed > 0 ? Math.ceil(beed) : Math.floor(beed)
      if (Height >= value) {
        clearInterval(time)
      } else {
        obj.style.height = Height + beed + 'px'
      }
    }, 1000 / 60)
  }
  Fans.prototype.inkt = function(obj,value){
    let time = null
    clearInterval(time)
    time = setInterval(()=> {
      let Height = obj.offsetHeight
      beed = (value - Height) / 20
      beed = beed > 0 ? Math.ceil(beed) : Math.floor(beed)
      if (Height <= value) {
        clearInterval(time)
      } else {
        obj.style.height = Height + beed + 'px'
      }
    }, 1000 / 60)
  }
  Fans.prototype.injt = function(){
    this.father.onmouseenter = () => {
      new Fans().init(this.box,150) 
    } 
  }
  Fans.prototype.inot = function(){
    this.father.onmouseleave = () => {
      new Fans().inkt(this.box,0) 
    }
  }
  // new Fans().init()  ------不能写，否则会自动执行
  new Fans().injt()
  new Fans().inot()
</script>
