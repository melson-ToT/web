# 一.for 循环---利用索引来循环它的对应的值：1.（i）代表索引 2.[i]代表值
var arr = [5,4,8]
for(var i = 0; i<= arr.length - 1;i++) {
    console.log(i,[i]);
    }

# 二.for in 循环---用来循环它的对象
var obj = {   ----for in 循环，循环它的属性名称，和属性值
      a: 1,
      b: 2,
      c: 3
}
for (var k in obj) {                 'k'： 代表随意一个数  
      console.log('k',k,obj[k]);      k ： 代表 obj 对象内的对象名称
    }                                 obj[k]： 代表 obj 对象内的对象的值

# 三.for of 循环---只能循环它数组内的值
var arr = [1,2,3]          ------for of循环，循环它的索引值，不要索引
    for (var j of arr) {      'j'：代表随意一个字母
      console.log('j',j);      j ：代表 arr 数组内的值
    }

# 四.forEach 循环数组的：---没有返回值（1.item:数组值、2.index:数组的索引、3.数组本身）
    var arr = [1,2,3]      ----不改变数组
    num = 0
    arr.forEach(function(item, index，arr) {
      if (item > 2) {
        num = item
        console.log('num',num); 
        console.log(item, index,arr); ---值、索引、数组本身
      }
    }
  );

# 五.formap 循环数组的：---有返回值（1.item:数组值、2.index:数组的索引、3.数组本身）
    var arr = [1,2,3]  ----改变原来的数组
    num = 0
    arr.formap(function(item, index，arr) {
      if (item > 2) {
        num = item
        console.log('num',num); 
        console.log(item, index,arr); ---值、索引、数组本身
      }
    }
  );

#  位置方法--indexOf()  lastIndexOf()返回要查找的项在数组中的索引位置,没找到则返回-1
var arr = ['apple','hello','hi','banana','hi','orange']

indexOf()方法从数组的开头开始向后查找
  console.log(arr.indexOf('hi')) //2

lastIndexOf()方法从数组的末尾开始向前查找
  console.log(arr.lastIndexOf('hi'))  //4

includes()查找存在
  console.log(arr.includes('hi'))  //true
  console.log(arr.includes('hehe'))  //false

数组去重
   var arr = [2,5,8,6,9,8,5,2,6,9]
 var newarr=[]
 for(var i = 0;i < arr.length;i++){
   if(newarr.indexOf(arr[i]) === -1){
     newarr.push(arr[i])
   }
 }
 console.log(newarr) //[2,5,8,6,9]

# 六.实现 +-\*/ 的案例
<body>
       <input type="text" id="n1">
       <input type="text" id="n2"> 
       <button id="t1">+</button>
       <button id="t2">-</button>
       <button id="t3">*</button>
       <button id="t4">/</button>
       <input type="text" id="n3">
  </body>
</html>
<script>
      t1.onclick=function(){
        n3.value = +n1.value + +n2.value
      }
      t2.onclick=function(){
        n3.value = +n1.value - +n2.value
      }
      t3.onclick=function(){
        n3.value = +n1.value * +n2.value
      }
      t4.onclick=function(){
        n3.value = +n1.value / +n2.value
      }
</script>

# 七.利用for循环进行数据对插
  <script>
     let arr = [{a: 1}, {b: 2}, {c: 3}]
     let brr = [{i: 4}, {j: 5}, {k: 6}]
     let crr = []
     for(let i=0;i<arr.length;i++){
       let drr = {...arr[i],...brr[i]}
       crr.push(drr)
     }
     console.log(crr);
  </script>


# 八.利用for map循环进行数据对插
var arr_1 = [{a: 1}, {b: 2}, {c: 3}]
var arr_2 = [{i: 4}, {j: 5}, {k: 6}]
var c=[]
var c= arr_1.map(function(item,index){
  return item = {...item,...arr_2[index]}
})
console.log(c);
</script>


# 九.对象转数组：
<script>
  let obj = {
    a:1,
    b:2
  }
  let arr = []
  for(let key in obj){
    arr.push({[key]: obj[key]})
  }
  console.log(arr);
</script>

# 十.数组转对象：
<script>
  let obj = {}
  let arr = [{a:1},{b:3},{c:5},{d:7},{e:9}]
  for (let i=0;i<arr.length;i++) {
    obj[i]=arr[i]
  }
  console.log(obj);
</script>



# 十一.Tab选项卡
    var oa = document.querySelectorAll('.ol li');
    var li = document.querySelectorAll('.ul li');
      oa.forEach((item, i)=> {
        oa[i].onmouseover = function(ev) {
          li[i].style.display = 'block';
          li[i].style.left = i * 300 + 'px'
        }
        oa[i].onmouseout = function() {
          li[i].style.display = 'none';
        }
      })
      var obj = {
        a: 2,
        b: 2,
      }
      for (var i in obj) {
        // a  obj.a
      }
      var arr = [3,4,5]
      for (var value of arr) {
        3,4,5
      }
   

