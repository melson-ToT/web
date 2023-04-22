# 一 定时器 :随机抽奖
  var n=['电视机','彩电','洗衣粉','谢谢惠顾','宝马汽车','笔记本电脑','水杯']
  var tame=window.setInterval(function(){       window.setInterval：定时器开始：
      var num=parseInt(Math.random()*n.length)   ：随机返回整数：                    
      box.innerHTML=n[num]                      box内容等于n的随机，索引范围内的内容
  },600)      
                                                       每600ms执行一次
  box.onclick=function(){
    window.clearInterval(tame)                     点击结束
  }

# 二，定时器：倒计时
<script>
  var n=document.querySelector('.box')           取div
  var timer=window.setInterval(function(){      window.setInterval：定时器开始：
    n.innerHTML--                               取box内的内容
    if(n.innerHTML==0){                         如果box内的内容等于0时
      window.clearInterval(timer)               结束(timer)的定时器
      n.style.display = 'none'
    } 
  },1000)
</script>

# 三，随机4到9之间的数字   -用封装函数
function fn(min, max) {
    return Math.round(Math.random() * (max - min)) + min;
  }        四舍五入        随机0~1
  console.log(fn(4, 9));
 
# 四.输出一个字符串的时间到页面上去
  function gatStringTime(){   gatString=将一字符串的形式  Time = 时间
    var a = new Date()        new Date()获取本地的时间
        var week = "";        等于字符串
    if (a.getDay() == 1) {
      week = "星期一";
    } else if (a.getDay() == 2) {
      week = "星期二";
    } else if (a.getDay() == 3) {
      week = "星期三";
    } else if (a.getDay() == 4) {
      week = "星期四";
    } else if (a.getDay() == 5) {
      week = "星期五";
    } else if (a.getDay() == 6) {
      week = "星期六";
    } else if (a.getDay() == 0) {
      week = "星期日";
    }
    return a.getFullYear()+'年'+(a.getMonth()+1)+'月'+a.getDate()+'日'+a.getHours()+':'+a.getMinutes()+':'+a.getSeconds()+'<br>'+'星期'+a.getDay()   本地时间的年、月、日、十分秒、星期
  }
  # document.body.innerHTML = getStringTime();   ---实现同步
  window.setInterval(function () {
    document.body.innerHTML = getStringTime();   body的内容===本地时间
  }, 1000);
  
# 五.双十一倒计时
var n = document.querySelector(".box");        1.获取HTML中的元素
  function s() {                               2.建立一个函数
    var a = new Date("2023-2-28 00:00:00");    3.设置一个未来时间
    var b = new Date();                        4.设置当前时间
    var c = Math.round((a - b) / 1000);        5.向下取整((未来时间-当前时间)/1000)
    var tian = parseInt(c / 86400);            6.计算天数
    var xiao = parseInt((c % 86400) / 3600);   7.计算小时
    var xi = xiao >= 10 ? xiao : "0" + xiao;   
    var fen = parseInt((c % 3600) / 60);       8.计算分钟
    var fe = fen >= 10 ? fen : "0" + fen;
    var miao = parseInt(c % 60);               9.计算秒数
    var mi = miao >= 10 ? miao : "0" + miao;
    return "距大甩卖只剩下:" + tian + "天" + xi + ":" + fe + ":" + mi;  10.组合天、时、分、秒
  }
  n.innerHTML = s();                           11.获取HTML中元素的内容=函数体--s()第十步
  window.setInterval(function () {             12.倒计时函数
    n.innerHTML = s();                         13.获取HTML中元素的内容=函数体--s()第十步
    if(n.innerHTML==="距大甩卖只剩下:"+'0'+'天'+'00:'+'00:'+'00'){  14.n的内容===结果时
      n.style.display='none'                   15.元素消失
    }
  }, 1000);                                    16.设置每一秒倒计时的时间
  
# 六，获取时间戳
    // 1.getTime方法获取
    // var d = new Date();
    // console.log(d.getTime()); //1642748482770 毫秒

## 七.背景图片代替当前的时间
  <body>
    <div>
      <img src="" alt="" />   取八个空img来对应时分秒的索引
      <img src="" alt="" />
      <img src="" alt="" />
      <img src="" alt="" />
      <img src="" alt="" />
      <img src="" alt="" />
      <img src="" alt="" />
      <img src="" alt="" />
    </div>
  </body>
</html>
<script>
  function imgTime() {
    var a = document.querySelectorAll("div img");
    var r = new Date();
    var Hours = r.getHours() >= 10 ? r.getHours() : "0" + r.getHours();
    var Minutes = r.getMinutes() >= 10 ? r.getMinutes() : "0" + r.getMinutes();
    var Seconds = r.getSeconds() >= 10 ? r.getSeconds() : "0" + r.getSeconds();
    var time = Hours + ":" + Minutes + ":" + Seconds;
    for (i = 0; i < a.length; i++) {
      if (i === 2 || i === 5) {   当time对应的：索引时，给图片：的样式
        a[i].src = "../img/img222/mh.png";
      } else {                    
        a[i].src = "../img/img222/" + time[i] + ".png";
      }      img的值（编号号码--图片9对应数字9）===图片内的内容为当前时间
    }
  }
  imgTime();
  window.setInterval(imgTime, 1000);
</script>

## 八.图片数字代替倒计时
<script>
  var a = document.querySelector("img");
  var n = 9;
  var b = window.setInterval(function () {
    a.src = "../img/img222/" + n + ".png";
    n--;
    if (n === 0) {
      window.clearInterval(b);
      a.style.display = "none";
    }
  }, 1000);
</script>

# 九.定时器弹出框消失
  <style>
    div {
      width: 200px;
      height: 100px;
      margin: 100px auto;
      line-height: 0;
      position: relative;
    }
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    span {
      background-color: #000;
      position: absolute;
      top: 8px;
      left: 70px;
      font-size: 12px;
      color: brown;
    }
  </style>
  <body>
    <div>
      <img src="../img/女好骚.png" alt="" />
      <span>距离下线时间只剩100秒</span>
    </div>
  </body>
</html>
<script>
  var a = document.querySelector("div span");
  var n = 100;                                  
  var b = window.setInterval(function () {
    a.innerHTML="距离下线时间只剩" + n + "秒";    
    n--;                                        
    if (n === 0) {                               
      window.clearInterval(b);
      a.style.display = "none";
    }
  }, 100);
</script>

# 十.DOM获取元素的值
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

二.延时定时器，规定的时间内执行一次
  setTimeout（函数名称，时间） 延时定时器，之执行一次
  clearTimeout(定时器的返回值) 停止定时
  <script> 
var a=window.setTimeout(function(){
  location.href='http://www.baidu.com'
},3000)

document.onclick=function(){ //关不关不重要
  window.clearTimeout(a)
}
</script>


