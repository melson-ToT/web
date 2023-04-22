# 一.回调函数的概念：
       ----回调函数做参数，传递给另外一个函数
比如：定时器，forEach,map...


# 二.回调函数的作用：
              ----可以获取函数内部的对象和数组

案例1.可以获取异步代码内部的值
<script>
function fn(cd){
  setTimeout(function(){
    let arr = [1,2,3]
    cd && typeof cd === 'function' && cd(arr)
  },0)
}
fn(function(a){
  console.log(a)
})
</script>


案例2.回调函数式解决异步顺序一种手段
#（非常重要）      ----这个案例可以决定那个异步先执行，
<script>
function fa(fb){
  setTimeout(function(){
    console.log('fa')
    fb && typeof fb === 'function' && fb()
  },1500)
}
function fb(){
  setTimeout(function(){
    console.log('fb')
  },500)
}
fa(fb)//fa在前，fb在后
</script>


# 三.封装函数的时候
           ----如果函数的参数比较多，参数的顺序容易出现问题
           ----封装的核心：对象做参数
           ----对象方便管理
案例1.
<script>
function fn(name,age,sex,obj,arr){
  console.log('你的姓名：'+ name)
  console.log('你的性别：'+ age)
  console.log('你的年龄：'+ sex)
  console.log('你的手机号：'+ obj)
  console.log('你的籍贯：'+ arr)
}
fn('张非','男',20,18756371756,'安徽')
</script>

解决方法：用对象的方式，对象是无序的
         如果函数的参数超过4个，尽量采用对象做参数，方便管理使用
案例2.
<script>
function fn(obj){
  console.log('你的姓名：'+ obj.name)
  console.log('你的性别：'+ obj.age)
  console.log('你的年龄：'+ obj.sex)
  console.log('你的手机号：'+ obj.date)
  console.log('你的籍贯：'+ obj.poot)
}
fn({
  name : '张非',
  age : '男',
  sex : '20',
  date : '18756371756',
  poot : '安徽'
})
</script>


# 四.封装函数实现ajax进行交互（获取数据）
<script>
function $ajax(obj){
  //1.默认配置的参数'get'
  obj = {
    type:obj.type || 'get',//请求的类型get或者post，默认是get
    url:obj.url,//地址的形参
    success:obj.success,//获取数据状态返回码成功的形参
    error:obj.error//获取数据状态返回码失败的形参
  }

  //2.1限定配置的获取属性
  if(!/^(get|post)$/.test(obj.type)){//限定请求方式如果不是get或post,提示错误
    throw new Error('仅支持get或post方式')//throw new Error=控制面板提示
  }
  //2.2限定配置的地址属性
  if(!obj.url){
    throw new Error('url地址必须填写')//throw new Error=控制面板提示
  }
  //3.ajax四部曲
  let xml = new XMLHttpRequest()
  xml.open(obj.type,obj.url,true)
  xml.send()
  xml.onreadystatechange = function(){
    if(xml.readyState === 4){
      let res =JSON.parse(xml.responseText)//首先用一个变量来接收这个实例的构造函数
      if(res.code===200){//如果变量的属性code===（3个等于是判断）200
        obj.success && typeof obj.success==='function' && obj.success(JSON.parse(xml.responseText))//则走这里
      }else{
        obj.error && typeof obj.error==='function' && obj.error('接口地址有误')
      }//否则，走这里
    }
  }
}
$ajax({
  type:'get',
  url:'http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10',
  success:function(data){ //success：成功的意思，自己遍，回调函数
    console.log(data)
  },
  error:function(err){//error：失败的意思，自己遍，回调函数
    console.log(err)
  }
})
</script>


# 五.封装函数实现ajax进行交互（发送数据）
            发送数据的请求：test/first
             'http://47.122.0.39:8000/api/positions/positionItem/?'
             'http://47.122.0.39:8000/test/first'          


    ---发送数据不是每次都需要：注册或购车类型的页面是需要的

1.ajax（get）发送数据：
<script>
  function $ajax(obj){
    type:obj.type
    url:obj.url

    let xml = new XMLHttpRequest()
    xml.open(obj.type,obj.url,true)
    xml.send()
    xml.onload = ()=>{
      let res = JSON.parse(xml.responseText)
      if(res.code===200){
        console.log(JSON.parse(xml.responseText))
      }else{
        throw new Error ('输入地址有误')
      }
    }
  }
  $ajax({
    type:'get',
    url:'http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10'
  })
</script>


2.ajax（post）发送数据：
<script>
  const obj = {
    name:'zhangsan',
    age:'20'
  }
  let arr = []                
  for (const key in obj) {     
    arr.push([key]+'='+obj[key]) 
  }
  arr.join('&')//name=zhangsan&age=20
  let xml = new XMLHttpRequest()
  xml.open('post','http://47.122.0.39:8000/test/first',true)
  xml.setRequestHeader('content-type','application/x-www-form-urlencoded')
  xml.send(arr.join('$'))                                        
  xml.onload = function(){
    console.log(JSON.parse(xml.responseText));
  }
</script>

