  # 一.promise的概述
       
    主要解决：多个数据接口的嵌套调用



  1.承诺的意思,解决回调地狱
  2.是一个异步的方法，同时是一个内置的构造函数
  3.写法：
<script>
  let pop = new Promise(function(resolve, reject){
    resolve()//将状态设为成功，()内可以携带参数
  })
  pop.then()   //是将resolve()设为成功，它会自动去找then()方法
  pop.catch()  //是将reject()设为失败，它会自动去找catch()方法
  pop.finally()//不管成功或失败，都会执行
</script>



# 二.promise的状态：
1.resolve：成功
2.reject：失败

（一）Promise 代表一个异步操作，有三种状态：pending进行中、fulfilled(resolve)成功、rejected失败。
（二）Promise 对象的状态改变有两种可能：从pending变为fulfilled和从pending变为rejected。

（三）一旦状态设定，就不会再变。承诺的意义



# 三.promise的简单操作

1. 如果状态设为成功，pop会自动找then()，then()方法依然是函数做参数，而且reject状态携带的数据给then()里面的参数

2. 如果状态设为失败，pop会自动找catch()，catch()方法依然是函数做参数，而且resolve状态携带的数据给catch()里面的参数

<script>
  let pop = new Promise(function( resolve, reject){
    resolve('hallo')//设置成功，内带参数
  })
  pop.then(function(e){//自动寻找then()方法，并把resolve()的实参数，传给then()的形参内
    console.log(e);
  })
  pop.finally(function(){
    console.log('不管成功或失败，都会执行')
  })
</script>

3. finally()：不管成功或失败，都会执行

4. then()、catch()、finally()就是promise实例对象的方法



# 四.promise取代回调函数的应用
<script>
  function fn() { //1.封装函数
    let pop = new Promise((resolve, reject) => { //2.变量获取promise(成功，失败)
      setTimeout(() => { 3.延时定时器
        let arr = ["zhangsan", "lisi", "wangwu"] //4.内部的数组
        resolve(arr)  //5.把数组放在成功的（）内     
      },1000)
    })
    return pop        //6.回给fn,return pop是重点
  }
  fn().then((res)=>{  //7.fn的then(res)为:["zhangsan", "lisi", "wangwu"]
    console.log(res); //8.回调fn内的arr
  })
</script>



# 五.promise的异步和then()可以多次链式调用

1.promise里面的代码是同步的，但是then()、catch()是异步的

2.promise里面的then()可以多次进行链式调用：
       fn().then().then()：允许then()内部还有then()的方法，称为链式

案例1.
<script>
function fn(){
  let pop = new Promise((resolve,reject)=>{
    resolve(100)
  })
  return pop
}
fn().then((res)=>{
   console.log('第一个res')//接收的是promise对象里面的resolve所携带的值100
}).then((res)=>{
   console.log('第二个res')//这里则显示undefined，因为这里的res是第二个res内部的参数
})//因为上一个res内部没有状态所以没有值
</script>

案例2.
<script>
  function fn() {
    let pop = new Promise((resolve, reject) => {
      resolve(100)
    })
    return pop
  }
  fn().then((res) => {
    console.log(res)//100
    return new Promise((resolve, reject) => {
      resolve(500)
    })
  }).then((sss) => {
    console.log(sss)//500
  })
</script>


# 五.promise封装（获取ajax）
<script>
  function $ajax(obj) {
    type: obj.type
    url: obj.url
    let promise = new Promise((resolve, reject) => {
      let xml = new XMLHttpRequest();
      xml.open(obj.type, obj.url, true);
      xml.send()
      xml.onreadystatechange = () => {
        if (xml.readyState === 4) {
          let res = JSON.parse(xml.responseText);
          if (res.code === 200) {
            resolve(res)
          } else {
            reject("接口地址有误")
            console.log(1)
          }
        }
      }
    })
    return promise
  }
  $ajax({
    type: "get",
    url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
  })
  .then(res => {
    console.log(res)
  })
  .catch(ree=>{
    throw new Error(ree)
  })
</script>


# 六.promise封装（发送ajax）
      
      get :
          1.如果不携带参数，则 域名+后端定义的路径（不用?）
          2.如果携带参数，则 域名+后端定义的路径+?+参数
          3.参数的对象一定转'name=zhangsan&age=20'格式
      post:
          1.如果携带参数，则 域名+后端定义的路径
          2.抬头请求（后端定义）
          3.send（）内，直接放对象


     ---发送数据不是每次都需要：注册或购车类型的页面是需要的



1.数组的模式
          ----但是用get传输数据不安全，尤其是密码
<script>
  let obj = new XMLHttpRequest()
  obj.open('get','http://localhost:8888/test.third?name=zhangsan&age=20',true)
  obj.send()
  obj.onload = function(){
    console.log(JSON.parse(obj.responseText));
  }
</script>

2.对象模式
<script>
  const obj = {
    name:'zhangsan',
    age:'20'
  }
  let arr = []                 1.准备一个数组来接收
  for (const key in obj) {     2.for.in来遍历对象内的属性
    arr.push(key+'='+obj[key]) 3.属性名 = 属性值，再push到arr的数组
  }
  arr//["name=zhangsan","age=20"]
  arr.join('&')//["name=zhangsan"&"age=20"]
  4.将arr内的两个属性用&来连接

  let obj = new XMLHttpRequest()
  obj.open('get','http://localhost:8888/test.third?'+arr.join('$'),true)
  obj.send()                                        5.将arr内的属性带进去
  obj.onload = function(){
    console.log(JSON.parse(obj.responseText));
  }
</script>


# 七.ajax（post）发送数据
          ----将数据放到send方法内传输
<script>
let obj = new XMLHttpRequest()
obj.open('post','http://localhost:8888/test.fourth',true)
obj.setRequestHeader('content-type','application/x-www-form-urlencoded')
1.send()方法之前必须要设置请求头
###可在html>body中<form action="" type="content-type,application/x-www-form-urlencoded"></form>，打出代码

obj.send('name=zhangsan$age=20')
2.将数据放到send方法内传输
obj.onload = function(){
  console.log(JSON.parse(obj.responseText));
}
</script>


# 八.利用promise解决地狱回调：
1. 获取两个或两个以上的接口数据，前提是第一个成功之后，获取第二个
2. promise获取多个接口数据，代码的可读性比回调函数合理一些

<script>
  function $ajax(obj) {
    type: obj.type
    url: obj.url
    let promise = new Promise((resolve, reject) => {
      let xml = new XMLHttpRequest();
      xml.open(obj.type, obj.url, true);
      xml.send()
      xml.onreadystatechange = () => {
        if (xml.readyState === 4) {
          let res = JSON.parse(xml.responseText);
          if (res.code === 200) {
            resolve(res)
          }
        }
      }
    })
    return promise
  }
  $ajax({
    type: "get",
    url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
  })
    .then(res => {
      console.log(res)//{code: 200, data: {…}, msg: "success", status: "success"}
      return $ajax({
        type: "get",
        url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
      })
    })
    .then(res => {
      console.log(res)//{code: 200, data: {…}, msg: "success", status: "success"}
    })
</script>


# 九.promise的静态方法：----这是回调函数不具备的

1. promise.all([实例对象])          ----多个实例对象一起执行，但每个都不能错
           1.同时获取多个数据的接口
           2.条件：每一个接口都不能出现错误，否则全错
           3.数组做参数
           4.参数为实例对象
           5.返回的是promise.all的一个数组

<script>
  function $ajax(obj) {
    type: obj.type;
    url: obj.url;
    let promise = new Promise((resolve, reject) => {
      let xml = new XMLHttpRequest();
      xml.open(obj.type, obj.url, true);
      xml.send();
      xml.onreadystatechange = () => {
        if (xml.readyState === 4) {
          let res = JSON.parse(xml.responseText);
          if (res.code === 200) {
            resolve(res);
          }
        }
      };
    });
    return promise;
  }
  let setPromise = Promise.all([
    $ajax({
      type: "get",
      url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
    }),
    $ajax({
      type: "get",
      url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
    }),
    $ajax({
      type: "get",
      url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
    }),
  ]);
  setPromise.then(res=>{
    console.log(res);//返回的是一个数组
  })
</script>



2. promise.race([实例对象])          ----那个先执行，后面的状态跟随先执行的
           1.同时获取多个数据的接口
           2.包装成一个新的promise实例对象
           3.数组做参数
           4.其中一个实例对象先执行，那么其他的实例对象跟着改变
           5.返回的是promise.all的一个数组

<script>
let p1 = new Promise((resolve,reject)=>{
  setTimeout(()=>{
    resolve(500);
  })
},500)
let p2 = new Promise((resolve,reject)=>{
  setTimeout(()=>{
    resolve(1000);
  })
},1000)
let p3 = new Promise((resolve,reject)=>{
  setTimeout(()=>{
    reject(1500);
  })
},1500)
let setpromise = Promise.race([p1,p2,p3])
setpromise.then(()=>{
  console.log('成功的');
})
.catch(()=>{
  console.log('失败的');
})
</script>


3. Promise.resolve()
          ----需要将对象转为Promise的对象，该方法起到这个作用
          ----返回一个新的Promise实例，将这个对象转为异步的
<script>
let p1 = 100
let p2 = Promise.resolve(p1).then((res)=>{
   console.log(res);//100  ,作用是将p1的数据变为异步的数据
})
</script>


4. Promise.reject()
          ----需要将对象转为Promise的对象，该方法起到这个作用
          ----返回一个新的Promise实例，将这个对象转为异步的
<script>
let p1 = 100
let p2 = Promise.reject(p1).catch((res)=>{
   console.log(res);//100  ,作用是将p1的数据变为异步的数据
})
</script>


# 十.try...catch...finally:
            ----容错处理（让错误不显示）
用途：兼容处理（if...else）
<script>
try{//如果第一条能走通，则走这里
   console.log(a);//如果走不通
} catch(e){//则走这里
   console.log(123);
}
</script>


# 十一.async和await
      ----解决回调地狱的终极方法
  // 1.async/await是一个 es8 的语法
<script>
  function $ajax(obj) {
    type: obj.type
    url: obj.url
    let promise = new Promise((resolve, reject) => {
      let xml = new XMLHttpRequest();
      xml.open(obj.type, obj.url, true);
      xml.send()
      xml.onreadystatechange = () => {
        if (xml.readyState === 4) {
          let res = JSON.parse(xml.responseText);
          if (res.code === 200) {
            resolve(res)
          }
        }
      }
    })
    return promise
  }
  async function fn() {
    let p1 = await $ajax({
      type: "get",
      url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
    })
    let p2 = await $ajax({
      type: "get",
      url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
    })
    let p3 = await $ajax({
      type: "get",
      url: "http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10",
    })
    console.log(p1)//{code: 200, data: {…}, msg: "success", status: "success"}
    console.log(p2)//{code: 200, data: {…}, msg: "success", status: "success"}
    console.log(p3)//{code: 200, data: {…}, msg: "success", status: "success"}
  }
  fn()
</script>





  // async 其实就是promise的语法糖。函数前面必须加一个async，异步操作的方法前加一个await 关键字。顾名思义，就是让你等一下，执行完了再继续往下走。注意：await 只能在async函数中执行，否则会报错。
 
  // 2.async:异步的意思，作用是申明一个异步函数，函数的返回值是promise 对象
  // async function fn() {}
  // console.log(fn());//返回的是promise对象
 
  // (async function(){}())
 
  // const fn = async () => { };
  // console.log(fn());//返回的是promise对象
 
  // 3.await:等待
  // - await是 async+wait 的结合 即异步等待，async和await 二者必须是结合着使用
  // - await就是promise里面then的语法糖。
  // - await直接拿到promise的返回值
  // - 最终的核心就是利用 async+wait 可以将异步代码写的和同步代码一样
 
  // $ajax({
  //   url: 'http://localhost:8888/goods/list',
  //   dataType: 'json'
  // }).then(res => {
  //   console.log(res);
  // });
 
 
  // async function fn() {
  //   let res = await $ajax({
  //     url: 'http://localhost:8888/goods/list',
  //     dataType: 'json'
  //   });
  //   console.log(res.list);
  // }
 
  // fn();//调用函数
 
  // 4.async和await回调地狱的终极解决方案
  // async function getData() {
  //   let res1 = await $ajax({
  //     url: 'http://localhost:8888/goods/list',
  //     data: {
  //       current: 1
  //     },
  //     dataType: 'json'
  //   });
 
  //   let res2 = await $ajax({
  //     url: 'http://localhost:8888/goods/list',
  //     data: {
  //       current: 2
  //     },
  //     dataType: 'json'
  //   });
 
  //   let res3 = await $ajax({
  //     url: 'http://localhost:8888/goods/list',
  //     data: {
  //       current: 3
  //     },
  //     dataType: 'json'
  //   });
 
 
  //   let res4 = await $ajax({
  //     url: 'http://localhost:8888/goods/list',
  //     data: {
  //       current: 4
  //     },
  //     dataType: 'json'
  //   });
 
  //   console.log(res1);
  //   console.log(res2);
  //   console.log(res3);
  //   console.log(res4);
  // }
 
  // getData();
 
 
  // 5.await取代then
  let p1 = new Promise((resolve, reject) => {
    resolve('我是resolve里面携带的数据1111111')
  });
 
  let p2 = new Promise((resolve, reject) => {
    resolve('我是resolve里面携带的数据22222222')
  });
 
  // p1.then(res => {
  //   console.log(res);
  // })
 
 
  async function fn() {
    // console.log(await p1);
    let res1 = await p1;
    let res2 = await p2;
    console.log(res1);
    console.log(res2);
  }
 
  fn();
</script>





       

