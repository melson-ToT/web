# 一.放大镜效果
布局：
    1.小盒子：小图片和小放大镜
    2.大盒子：大图片和大放大镜
    3.所有的盒子、图片、放大镜都是正方形
    4.大盒子与小盒子、大图片与小图片、大放大镜与小放大镜的比例一致
    5.给小放大镜一个visibility: hidden;占位隐藏
    6.鼠标移入时，给小放大镜visibility='visible'占位出现
    7.小图片的移动和大图片的移动是相反的，大图片的left和top前面加负数
##  8.鼠标移入事件、鼠标移动事件、鼠标移出事件一定要给父元素

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<style> 
  *{
    margin: 0;
    padding: 0;
  }
  .father {
    margin: 50px 0 0 50px;
  }
  .box {
    width: 300px;
    height: 300px;
    float: left;
    position: relative;
  }
  .xiaotu {
    width: 100%;
    height: 100%;
  }
  .xijing {
    width: 200px;
    height: 200px;
    background-color: blue;
    opacity: 0.3;
    position: absolute;
    top: 0;
    left: 0;
    visibility:hidden;
  }
  .dajing {
    width: 400px;
    height: 400px;
    position: relative;
    overflow: hidden;
    float: left;
  }
  .datu {
    width: 600px;
    height: 600px;
    position:absolute;
    top: 0;
    left: 0;
  }
  </style>
  <body>
    <div class="father">
      <div class="box">
        <img src="../img/女好骚.png" alt="" class="xiaotu">
        <div class="xijing"></div>
      </div>
      <div class="dajing">
        <img src="../img/女好骚.png" alt="" class="datu">
      </div>
    </div>
  </body>
  </html>
  </html>
  <script>
   function Fath(){
    this.father = document.querySelector('.father')
    this.box = document.querySelector('.box')
    this.xiaotu = document.querySelector('.xiaotu')
    this.xijing = document.querySelector('.xijing')
    this.dajing = document.querySelector('.dajing')
    this.datu = document.querySelector('.datu')
   }
   Fath.prototype.init = function(){
    this.box.onmouseenter = ()=>{
      this.xijing.style.visibility = 'visible'
      this.box.onmousemove = (e)=>{
        let leftvalue = e.clientX - this.father.offsetLeft - this.xijing.offsetWidth/2
        let topvalue = e.clientY - this.father.offsetTop - this.xijing.offsetHeight/2
        if(leftvalue <=0){
          leftvalue = 0
        }else if(leftvalue >= this.xiaotu.offsetWidth - this.xijing.offsetWidth){
          leftvalue = this.xiaotu.offsetWidth - this.xijing.offsetWidth
        }
        if(topvalue <=0){
          topvalue = 0
        }else if(topvalue >= this.xiaotu.offsetHeight - this.xijing.offsetHeight){
          topvalue = this.xiaotu.offsetHeight - this.xijing.offsetHeight
        }
        this.xijing.style.left = leftvalue + 'px'
        this.xijing.style.top = topvalue + 'px'
        this.datu.style.left = -leftvalue*(this.datu.offsetWidth / this.xiaotu.offsetWidth) + 'px'
        this.datu.style.top = -topvalue*(this.datu.offsetWidth / this.xiaotu.offsetWidth) + 'px'
      }
    }
    this.box.onmouseleave = ()=>{
      this.xijing.style.visibility = 'hidden'
    }
   }
   new Fath().init()
  </script>