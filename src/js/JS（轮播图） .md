# 一 轮播图：
1. 8个小圆圈对应8张图片，鼠标移入进行图片的切换
2. 点击左右箭头，按照左右进行图片的切换
3. 图片自动轮播-定时器
<style>
  *{
    margin: 0;
    padding: 0;
  }
  .father {
    width: 400px;
    height: 400px;
    position: relative;
    margin: 20px auto;
    border: 1px black solid;
    box-sizing: border-box;
  }
  li {
    list-style: none;
  }
  ul {
    width: 100%;
    height: 100%;
    display: flex;
  }
  ul li {
    width: 100%;
    height: 100%;
    line-height: 0;
    display: none;
  }
  ul li img{
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  ul li:nth-child(1) {
    display: block;
  }
  ol {
    position: fixed;
    left: 206px;
    top: 362px;
    z-index: 10;
    display: flex;
  }
  ol li {
    width: 30px;
    height: 30px;
    background-color: blue;
    border-radius: 15px;
    margin-right: 10px;
  }
  ol li.active{
    background-color: red;
  }
  .L {
    width: 100px;
    height: 100px;
    position: fixed;
    top: 158px;
    left: 159px;
  }
  .R {
    width: 100px;
    height: 100px;
    position: fixed;
    top: 158px;
    left: 508px;
  }
</style>
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
    </ul>
    <ol>
      <li class="active"></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ol>
    <div class="son">
      <img src="../img/img222/ll.png" alt="" class="L">
      <img src="../img/img222/RR.png" alt="" class="R">
    </div>
  </div>
</body>
</html>
</html>
<script>
const father = document.querySelector('.father')
const ulli = document.querySelectorAll('ul li')
const olli = document.querySelectorAll('ol li')
const L = document.querySelector('.L')
const R = document.querySelector('.R')
var index = 0                                1.变量=index = 0
for(i=0;i<olli.length;i++){                  2.循环olli索引
  olli[i].index=i                            3.olli的所有索引值的属性=所有索引（）
  olli[i].onmouseenter = function(){         4.点击olli的li时
    for(j=0;j<olli.length;j++){              5.循环olli的索引
      olli[j].className=''           6.olli的索引的class名为空的时候，olli的索引颜色为默认颜色
      ulli[j].style.display='none'           7.ulli的索引的class为空的时候，olli的索引全部消失
    }
      this.className='active'    8.鼠标移入olli谁的索引的class名为active的时候，谁的颜色改变
      ulli[this.index].style.display='block'    9.ulli的索引[olli对应的i]的li出现
      index = this.index                    10.index（ulli的li）=当前的olli的li
  }
}
L.onclick = function(){
  index--                                   11.ulli的li--
  if(index<0){                              12.如果ulli的索引<0时
    index=olli.length - 1                   13.ulli的索引=ulli最后一个索引
  }
  for(i=0;i<ulli.length;i++){               14.循环ulli的li
    olli[i].className=''           15.olli的索引的class名为空的时候，olli的索引颜色为默认颜色
    ulli[i].style.display='none'            16.ulli的索引的class为空的时候，olli的索引全部消失
  }
  ulli[index].style.display='block'         17.ulli[当前的li]出现
  olli[index].className='active'            18.olli[当前li].class名='active'，颜色改变
}
R.onclick = function(){
  index++
  if(index>olli.length - 1){
    index=0
  }
  for(i=0;i<ulli.length;i++){
    olli[i].className=''
    ulli[i].style.display='none'
  }
  ulli[index].style.display='block'
  olli[index].className='active'
}
var time=setInterval(function(){                 
   R.onclick()                        1.右键的点击事件
 },3000)
father.onmouseenter = function(){
  clearInterval(time)                 2.关闭定时器
}
father.onmouseleave = function(){     3.鼠标移入时
  time=setInterval(function(){        4.定时器继续执行开始
   R.onclick()
 },3000)
}
</script>


### 轮播图
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
}
ul {
  width: 100%;
  height: 100%;
  float: left;
  padding: 0;
}
ul li{
  width: 100%;
  height: 100%;
  float: left;
  list-style: none;
  display: none;
}
ul li img{
  width: 100%;
  height: 100%;
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
 <script>
const father = document.querySelector('.father') 
const uli = document.querySelectorAll('ul li')
const oli = document.querySelectorAll('ol li')
const left = document.querySelector('.left')
const right = document.querySelector('.right')
let time = null
let index = 0
for(let i=0;i<oli.length;i++){
  oli[i].onmouseenter = function(){
    for(let j=0;j<oli.length;j++){
    oli[j].className = ''
    uli[j].style.display = 'none'
    }
    this.className = 'ccc'
    uli[i].style.display = 'block'
  }
}
left.onclick = function(){
  index--
  if(index<0){
    index = oli.length - 1
  }
  for(let j=0;j<oli.length;j++){
    oli[j].className = ''
    uli[j].style.display = 'none'
    } 
  oli[index].className = 'ccc'
  uli[index].style.display = 'block'
}
right.onclick = function(){
  index++
  if(index>oli.length - 1){
    index = 0
  }
  for(let j=0;j<oli.length;j++){
    oli[j].className = ''
    uli[j].style.display = 'none'
    } 
  oli[index].className = 'ccc'
  uli[index].style.display = 'block'
}
time = setInterval(function(){
  right.onclick()
},3000)
father.onmouseover = function(){
  clearInterval(time)
}
father.onmouseleave = function(){
  time = setInterval(function(){
  right.onclick()
},3000)
}
</script>

