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

# 四，日期对象
   1.和本地日期时间有关
   2.输出当前的日期、设置未来的日期、倒计时
   var r=new Date
   console.log(r)   Fri Feb 24 2023 21:55:05 GMT+0800 (中国标准时间)

   console.log(r.toLocaleString())  2023/2/24 下午9:55:05

   console.log(r.getFullYear())  2023 年

   console.log(r.getDate())  24  日

   console.log(r.getDay())  5  星期

   console.log(r.getHours() + ":" + r.getMinutes() + ":" + r.getSeconds());  22:9:32 时分秒

# 五.放置时间为个位时，则前面加0  
  var r=new Date()
  var Hours = r.getHours() >= 10 ? r.getHours() : '0'+ r.getHours()
  var Minutes = r.getMinutes() >= 10 ? r.getMinutes() : '0'+ r.getMinutes()
  var Seconds = r.getSeconds() >= 10 ? r.getSeconds() : '0'+ r.getSeconds()
  console.log(Hours + ":" + Minutes + ":" + Seconds); 

# 六.输出一个字符串的时间到页面上去
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
  
# 七.设置日期-忽略星期
1.数字方式设置：---月份可以进位 new Date(2022, 13, 26, 14, 28, 00)
             月份自动+1，设置时间月份时-1
  var date = new Date(2023, 1, 26, 14, 28, 00); //2023/2/26 下午2:28:00
  console.log(date.toLocaleString());

  2.字符串方式设置
             月份正常使用，不会-1和进位
  var date = new Date('2023-2-26 14:26:00'); //2023/2/26 下午2:28:00
  console.log(date.toLocaleString());

  3.利用日期对象的方法进行重新设置日期---可以进位
  # getDate---获取日期
  # setDate---设置日期
  var date = new Date();---2023/2/26 下午2:57:30
       日期     当前日期
  date.setDate(date.getDate()+10)---2023/3/8 下午2:57:30  天数计算方法
      设置日期      获取日期    天数
  console.log(date.toLocaleString());
              日期   .toLocaleString() 函数用于将当前对象以字符串值的形式返回  

  ### 年、月、日、星期、时分秒 的设置方法
  date.setFullYear(date.getFullYear()+10)---年数计算方法
  date.setMonth(date.getMonth()+9)---月份计算方法（-1）
  date.setDate(date.getDate()+10)---天数计算方法
  date.setDay(date.getDay()+10)---星期计算方法
  date.setHours(date.getHours()+10)---小时计算方法
  date.setMinutes(date.getMinutes()+10)---分钟计算方法
  date.setSeconds(date.getSeconds()+10)---秒数计算方法

# 八.双十一倒计时
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
  
# 九.获取元素对象
    <body>
    <ul>
      <li>11111</li>
      <li>22222</li>
      <li>33333</li>
      <li>44444</li>
      <li>55555</li>
    </ul>
    <ol>
      <li>66666</li>
      <li>77777</li>
      <li>88888</li>
      <li>99999</li>
      <li>00000</li>
    </ol>
  </body>
 <script>
  1.获取单个元素---document.querySelector("元素名或选择器")
  var a=document.querySelector('ul li:nth-of-type(2)')  ul的第二个li
  console.log(document.querySelector('ul li'))   ul的第一个li
  console.log(document.querySelector('ul li:nth-of-type(3)'))  ul的第三个li

  2.获取多个元素---document.querySelector('ul li')  
  利用索引下标选择想要的元素
  var a = document.querySelectorAll("ul li");
  console.log(document.querySelectorAll('ul li'))---ul的所有li
  console.log(document.querySelectorAll('ul li')[0]) ---ul索引0位置的li
  console.log(a[0].innerHTML);//1111
</script>  

# 十，获取时间戳
    // 1.getTime方法获取
    // var d = new Date();
    // console.log(d.getTime()); //1642748482770 毫秒

## 十一。背景图片代替当前的时间
<div>
      <p>0</p>
      <p>0</p>
      <p>:</p>
      <p>0</p>
      <p>0</p>
      <p>:</p>
      <p>0</p>
      <p>0</p>
    </div>
  </body>
</html>
<script>
  function p() {
    var a = document.querySelectorAll("div p");
    var r = new Date();
    var Hours = r.getHours() >= 10 ? r.getHours() : "0" + r.getHours();
    var Minutes = r.getMinutes() >= 10 ? r.getMinutes() : "0" + r.getMinutes();
    var Seconds = r.getSeconds() >= 10 ? r.getSeconds() : "0" + r.getSeconds();
    var time = Hours + ":" + Minutes + ":" + Seconds;
    for (i = 0; i < a.length; i++) {
      if (i === 2 || i === 5) {
        a[i].innerHTML = a[i].innerHTML  或time[i];  因为a的索引位置2(：)刚好对应time索引位2(：)置：
      } else {
        a[i].innerHTML = time[i];
      }
    }
  }
  p();
  window.setInterval(p, 1000);
</script>

## 十二。背景图片代替当前的时间
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

## 十三。图片数字代替倒计时
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

# 十四.定时器
一.间隔定时器--反复执行
  setInterval(函数名称，时间)  间隔定时器
  clearInterval(定时器的返回值) 停止定时

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



  




                         
