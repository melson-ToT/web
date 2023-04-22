###
# 一.数组去重：splice
    var arr = [12, 12, 12, 12, 3, 3, 3, 4, 5, 12, 3, 4, 5, 5, 5, 6, 7, 123];
    for (var i = 0; i < arr.length; i++) {
        for (var j = i + 1; j < arr.length; j++) {
            if (arr[i] === arr[j]) {
                arr.splice(j, 1); 
                j--; 减去最后的索引
            }
        }
    }
    console.log(arr); //[12, 3, 4, 5, 6, 7, 123]

# 二.数组去重：push
  var n = [2, 5, 8, 2, 5, 8, 2, 5, 8];
  var x = [];
  for (var i = 0; i < n.length; i++) {
    flag = 1;
    for (var j = 0; j < x.length; j++) {  x的长度
      if (n[i] === x[j]) {  
        flag = 2;
      }
    }
    if (flag === 1) {
      x.push(n[i]);
    }
  }
  console.log(x);

# 三，数组去重----indexOf()方法
# 位置方法--indexOf()  lastIndexOf()返回要查找的项在数组中的索引位置,没找到则返回-1
var arr = ['apple','hello','hi','banana','hi','orange']
         ----indexOf()方法从数组的开头开始向后查找
  
 var arr = [2,5,8,6,9,8,5,2,6,9]
 var brr=[]
 for(var i = 0;i < arr.length;i++){
   if(brr.indexOf(arr[i]) === -1){
     brr.push(arr[i])
   }
 }
 console.log(brr) //[2,5,8,6,9]

# 四.倒计时方法
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

# 五.图片切换案例 
<style>
    .fahter {
      width: 400px;
      height: 400px;
      box-sizing: border-box;
      margin: 100px auto;
      position: relative;
    }
    #pic {
      width: 400px;
      height: 400px;
      object-fit: cover;
    }
    #l {
      width: 100px;
      height: 100px;
      position: absolute;
      left: -100px;
      top: 150px;
    }
    #r {
      width: 100px;
      height: 100px;
      position: absolute;
      right: -100px;
      top: 150px;
    }
  </style>
  <body>
    <div class="fahter">
      <img src="../img/1.png" alt="" id="pic" />
      <img src="../img/l.png" alt="" id="l">
      <img src="../img/r.png" alt="" id="r">
    </div>
  </body>
</html>
<script>
    var num = 1
    r.onclick = function () {
      num ++
      if (num > 4) {
        num = 1 
      }
      // pic.src = "../img/" + num + ".png"
      pic.src = `../img/${num}.png`
    }
    l.onclick = function () {
      num --
      if (num < 1) {
        num =4
      }
      pic.src = "../img/" + num + ".png"
    }
</script>

# 六.==考试案例  判读是星期几
<script>
  var xiqi = prompt("请输入星期：");
  switch (+xiqi) {
    case 1:
    console.log("今天星期一");
      break;
    case 2:
    console.log("今天是星期二");
      break;
    case 3:
    console.log("今天是星期三");
      break;
    case 4:
    console.log("今天是星期四");
      break;
    case 5:
    console.log("今天是星期五");
      break;
    case 6:
    console.log("今天是星期六");
      break;
    case 7:
      console.log("今天是星期天");
      break;
    default:
    console.log('输入有误')
    break
  }
</script>

# 七.while循环的练习
     案例1：绘制10*10表格(table,tr,td)
   <script>
  document.write('<table width=400px heith=400px border=1 cellspacing="0">')
    var a = 1
    while(a<=10){
      document.write('<tr></tr>')
      a++
      console.log(123,a)
      b=1
      while(b<=10){
        document.write('<th>77777</th>')
        b++
        console.log(145,b)
      }
    }
  document.write('</table>')
</script>

# 八.冒泡排序，两两比较，从小到大
<script>
  var a=[5,2,3,6,8,2,6,8,5,6]
  for (var i=0;i<a.length;i++){
    for(var j=0;j<a.length;j++){
      if(a[j]>a[j+1]){
        var timp=a[j]
            a[j]=a[j+1]
            a[j+1]=timp
      }
    }
  }
  console.log(a)

# 九.sort排序
<script>
var x=[8,7,3,4,5,6]
x.sort(function(a,b){return a-b})
  console.log(x)

#  利用split 拆分数组： 将字符串'get - element-by-id'转换成数组
   var arr = 'get - element-by-id'
   console.log(arr.split('-')) //  (4) ["get ", " element", "by", "id"]

# 利用正则
   var arr = 'aaabbbbcccdddffffeee'
   var brr = /(\w)\1*/g
   var crr = {}
   arr.replace(brr,function(a,b){
    console.log(a);
    console.log(a.length);
    console.log(b);
    crr[b]= a.length
   })
   console.log(crr)

# 十.用
# 案例1：new Set方法
<script>
let arr = ['zhangsan','lisi',100,200,'zhangsan','lisi',100,200]
console.log(new Set(arr))       //   Set(4) {"zhangsan", "lisi", 100, 200}
console.log([...new Set(arr)])  //   (4) ["zhangsan", "lisi", 100, 200]
</script>
   