  # 一.cookie的概述：
  1. 回话跟踪技术，有web服务器保存在用户浏览器上的小文本文件，它包含用户的信息
  2. cookie存储的数据首饰字符串的格式
  3. cookie的作用就是将，注册和登录页面的用户信息保存到cookie内，可以跨页面访问

  # 二.cookie的存储+过期时间
  1.存储方式document.cookie = 'key = value'
                      键    值
  2.每次存储一条，cookie的大小不能超过4kb，可以携带过期时间

  3.代码书写后，右键点击 Alt+O

<script>
let time = new Date              1.当前时间
time.setDate(time.getDate()+10)  2.time.设置时间（time.获取当前时间+10）
document.cookie = 'name = zhangsan,expires = time'
            3.expires = time 保存cookie为当前时间+10天----过期时间
</script>


# 三.cookie的存储，如果不同的目录cookie是不能相互访问的
1. 所以要配置路径
2. 将cookie存储的路径设置为根目录 pash = /  ,就可以任意访问cookie了
<script>
  let time = new Date            
  time.setDate(time.getDate()+10) 
  document.cookie = 'name = zhangsan;expirres = time;pasn = /'          
 </script>                                       4.pasn = / 储存在根目录


# 四.cookie的存储的封装函数
<script>
function setCookie(key,value,Day){
  let time = new Date
  time.setDate(time.getDate()+Day)
  document.cookie =  `${key} = ${value};expires = ${time}time;path = /`
}                                              
setCookie('name','zhangsan',10)
</script>   

# 五.cookie对象格式的存储的封装函数
       ----通过JSON.stringify方法
<script>
let obj= {
  a:1,
  b:2,
  c:3
}
function setCookie(key,value,Day){
  let time = new Date
  time.setDate(time.getDate()+Day)
  document.cookie = `${key} = ${value};expires = ${time};pasn = /`
}
setCookie('name',JSON.stringify(obj),10)
</script>


# 六.cookie的获取和封装
<script>
function setCookie(key,value,Day){
  let time = new Date
  time.setDate(time.getDate()+Day)
  document.cookie =  `${key} = ${value};expires = ${time};path = /`
}                                              
setCookie('name','zhangsan',10)
setCookie('age','lisi',10)
setCookie('sex','wangwu',10)
function getCookie(key){                1.设置函数，
  let arr = document.cookie.split('; ') //['name'='zhangsan','age'='lisi','sex'='wangwu']
  2.arr的数组=取存放的所有cookie，这里注意分号后面多一个空格加空格
  for (let value of arr) {     3.for of遍历数组，将一个数组，变成三个
    let brr = value.split('=')  4.brr拆分，拆成数组的第一项都是key，第二项都是值
    if(brr[0] = key){           5.如果brr的索引1值 = 输入的属性
      return brr[1]              6.就返回，brr的第二个索引值
    }
  }
}
console.log(getCookie('name'));         7.打印getCookie('name')，就会返回name的值//张三
</script>    



# 七.cookie的删除
1.设置过期时间，如果到了设置的时间cookie，自动消失

2.cookie的key值如果是重名，则下面的覆盖上面的

3.自定义函数删除:
<script>
let obj = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 'wangwu'
}
function setCookie(key,value,Day){
  let time = new Date()
  time.setDate(time.getDate()+Day)
  document.cookie = `${key} = ${value};expires = ${time};pash =/`
}
setCookie('name','zhangsan',10)
setCookie('age','lisi',10)
setCookie('sex','wangwu',10)
function delCookie(key){    1.设置函数
  setCookie(key,'',-1)      
  2.将创建的setCookie（）内的参数带入，如果是重名则覆盖，-1+当前的时间就一定会过期
} 3.先那个属性，先覆盖，再让这个时间过期
delCookie('name')
</script>    


# 八，本地存储的方法： localStorage存放在浏览器的本地，永久性保存

1. 存 -- localStorage.setItem()
<script>
localStorage.setItem('name','zhangsan')
console.log(localStorage.setItem('name'));//zhangsan
</script> 

 如果是对象的形式,必须先转为--JSON.stringify()的格式
<script>
  let obj = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 'wangwu'
}
localStorage.setItem('abc',JSON.stringify(obj))
</script> 

2. 取 -- localStorage.getItem()
<script>
localStorage.setItem('name','zhangsan')
localStorage.getItem('name')
console.log(localStorage.getItem('name'));//zhangsan
</script>  

如果取的是对象格式的则转为：JSON.stringify()的格式
<script>
  let obj = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 'wangwu'
}
localStorage.setItem('abc',JSON.stringify(obj))
JSON.parse(localStorage.getItem('abc'))
console.log(JSON.parse(localStorage.getItem('abc')));
//{name: "zhangsan", age: "lisi", sex: "wangwu"}
</script>  

3. 删 -- localStorage.removeItem()
<script>
localStorage.setItem('name','zhangsan')
localStorage.setItem('age','男')
localStorage.setItem('sex','20')
localStorage.removeItem('name')//name被删除
</script>  

4. clear方法，清空本地存储
<script>
localStorage.setItem('name','zhangsan')
localStorage.setItem('age','男')
localStorage.setItem('sex','20')
localStorage.clear()  //清空所有的存储内容
</script>    

           

  
