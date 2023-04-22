
# 三.抛物线  ----定点抛物线
1. 重点：抛物线的公式：
    y = a*x*x + b*x + c （三个未知数a,b,c  位置：x,y:目标位置和起始位置的差值）

2. 根据公式的规则，如果起始位置当做原点：c=0

3. 公式变化：y = a*x*x + b*x(两个未知数a,b)

4. a:曲线，抛物线的孤独，浏览器尺寸有限，值需要自行定义（0.002~0.009）

5. 公式变化：已知x,y差值，已知a曲线，求b
   b = （y - 0.002*(两者之间的left差值)*(两者之间的left差值)) / (两者之间的left差值)
.box1 {
  width: 100px;
  height: 50px;
  background-color: blue;
  position: absolute;
  left: 400;
  top: 200px;
}
.box2 {
  width: 100px;
  height: 50px;
  background-color: blue;
  position: absolute;
  left: 400px;
  top: 400px;
}

</style>
<body>  
<div class="box1"></div>
<div class="box2"></div>
 </body>
 </html>
 </html>
 <script>
const box1 = document.querySelector('.box1')
const box2 = document.querySelector('.box2')
let time = null
box1.onclick = function(){
    clearInterval(time)
    let box1_po = {
      left:box1.offsetLeft,
      top:box1.offsetTop
    }
    let dis = {
      x:box2.offsetLeft - box1_po.left,
      y:box2.offsetTop - box1_po.top
    }
    let a = 0.002
    let b = (dis.y - a*dis.x*dis.x) / dis.x 
    let x = 0
    time = setInterval(function(){
      x+=4
      if(box1.offsetLeft>=box2.offsetLeft){
        clearInterval(time)
      }else{
        box1.style.left = box1_po.left + x +'px'
        box1.style.top = box1_po.top + a*x*x + b*x +'px'
      }
    },1000 / 60)
}
</script>

# 四.圆周运动                  
let x = a+Math.con(get*Math.PI / 180) * r
let y = b+Math.sin(get*Math.PI / 180) * r
x,y:盒子的位置
a,b:圆心的位置
r:半径
get：角度

# 五.购物车抛物线：
  <style>
*{
  margin: 0;
  padding: 0;
}
.father{
  margin: 100px auto;
  width: 600px;
  height: 400px;
  border: 1px black solid;
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.box1 {
  width: 100px;
  height: 50px;
  background-color: blue;
}
.box2 {
  width: 100px;
  height: 50px;
  background-color: blueviolet;
  margin-top: 350px;
}
.son {
  width: 20px;
  height: 20px;
  background-color: red;
  position: absolute;
  top: 175px;
  left: 80px;
  border-radius: 50%;
}
</style>
 <body>
  <div class="father">   
    <div class="box1"></div>
    <div class="box2"></div>
    <div class="son"></div>
  </div>
 </body>
 </html>
 </html>
 <script>
const box1 = document.querySelector('.box1')
const box2 = document.querySelector('.box2')
const son = document.querySelector('.son')
let time = null
box1.onclick = function(){
  clearInterval(time)
    let left = son.offsetLeft
    let top = son.offsetTop
    let x = box2.offsetLeft - left
    let y = box2.offsetTop - top
        let a = 0.002
    let b = (y - a*x*x) / x 
    let n = 0
    time = setInterval(function(){
      n+=4
      if(son.offsetLeft>=box2.offsetLeft){
        clearInterval(time)
      }else{
        son.style.left = left + n +'px'
        son.style.top = top + a*n*n + b*n +'px'
      }
    },1000 / 60)
}

# 六.购物车抛物线
*{
  margin: 0;
  padding: 0;
}
.father{
  margin: 100px auto;
  width: 600px;
  height: 400px;
  border: 1px black solid;
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.box1 {
  width: 100px;
  height: 50px;
  background-color: blue;
}
.box2 {
  width: 100px;
  height: 50px;
  background-color: blueviolet;
  margin-top: 350px;
}
.son {
  width: 20px;
  height: 20px;
  background-color: red;
  position: absolute;
  top: 175px;
  left: 80px;
  border-radius: 50%;
  opacity: 0;                13.先设置透明度为0
}
</style>
 <body>
  <div class="father">   
    <div class="box1"></div>
    <div class="box2"></div>
    <div class="son"></div>
  </div>
 </body>
 </html>
 </html>
 <script>
const box1 = document.querySelector('.box1')
const box2 = document.querySelector('.box2')
const son = document.querySelector('.son')
let time = null
box1.onclick = function(){
  clearInterval(time)                     5.防止定时器叠加速度
    let left = son.offsetLeft             1.获取son的left的变量
    let top = son.offsetTop               2.获取son的top的变量
    let x = box2.offsetLeft - left        3.获取两者之间差left变量
    let y = box2.offsetTop - top          4.获取两者之间差left变量    
    let a = 0.002                         6.获取抛物线的曲线
    let b = (y - a*x*x) / x               7.获取抛物线的方程式
    let n = 0                             8.获取抛物线的速度
    time = setInterval(function(){
      n+=10                               9.设置抛物线速度的叠加
      if(son.offsetLeft>=box2.offsetLeft){10.当抛物线到达目的地时
        clearInterval(time)               11.消除定时器
        son.style.opacity=0               15.当盒子到达位置时，设置透明度为0
      }else{
        son.style.opacity=1               14.当盒子飞行过程中，设置透明度为1
        son.style.left = left + n +'px'
        son.style.top = top + a*n*n + b*n +'px'
        12.如果抛物线没有到达时，它的位置=不断获取运动的位置+叠加位置
      }
    },1000 / 60)
}
</script>

