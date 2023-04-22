  # 域名地址：
           http://47.122.0.39:8000/api/positions/positionItem/?pageNum=1&pageSize=10

           ajax四部曲的cdn，js地址
             <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>

  # 一.ajax的概述
   ajax 全名 async javascript and XML
   异步的javascript和xml
   1.异步(async)的意义
   javascript是单线程的(只有一个主线程，所有的任务的都是在主线程完成)，同步和异步在主线程上面执行的顺序。
   同步：阻塞模式，后一个任务等到前一个任务完成，同步代码进入主线程进行执行。
   console.log(1);
   console.log(aaaaaa);
   console.log(2);
   console.log(3);
 
   异步：非阻塞模式，异步代码先进入队列里面，不进入主线程，等到主线程上面的同步代码完成，被通知执行。
   定时器是异步的(异步主要指的是里面的函数)
   console.log(1);//同步
   setTimeout(function () {//异步的，进队列
     console.log(2);
   }, 0);
   setTimeout(function () {//异步的，进队列
     console.log(3);
   }, 1000);
   console.log(4);//同步
   1,4,2,3
 
   2.XML：可扩展的标签语言，类似于HTML，区别是XML里面的标签可以自定义的，是早期的一种数据格式，当前已经被JSON取代了。
   xml需要声明
   xml标签成对出现，必须设置一个根节点。
 
 
 
   二.ajax的特点
   1.ajax直接使用，不需要插件的支持，原生 js 就可以使用
   2.用户体验好
   3.减轻服务端和带宽的负担(ajax实现了前后端的分离)
   4.缺点：搜索引擎的支持度不够，因为数据都不在页面上，搜索引擎搜索不到

 
   三.AJAX 的使用
   1.在 js 中有内置的构造函数来创建 ajax 对象
   2.创建 ajax 对象以后，我们就使用 ajax 对象的方法去发送请求和接受响应
</script>


# 二.ajax四部曲：
   一.AJAX 的使用
   1.在 js 中有内置的构造函数来创建 ajax 对象
   2.创建 ajax 对象以后，我们就使用 ajax 对象的方法去发送请求和接受响应
 
   二.AJAX 的四步曲获取接口数据
   1.第一步：利用内置的构造函数(XMLHttpRequest)创建ajax对象
   let xhr = new XMLHttpRequest();
 
    2.第二步：利用ajax对象下面的open方法打开或者连接通讯的接口
    open的三个参数
    参1：请求方式get查,post增,put改,delete删...
    参2：接口地址url
    参3：是否异步，true异步，false同步
   xhr.open('get', 'http:localhost:8888/goods/list', true);
 
    3.第三步：利用ajax对象的send方法发送解析(但过程比较复杂)
    发送解析的过程比较复杂，有下面的5步组成，必须等到最后一步完成，可以获取对应的接口数据。
    xhr.readyState表示就绪状态码
    - readyState === 0： 表示未初始化完成，也就是 `open` 方法还没有执行
    - readyState === 1： 表示配置信息已经完成，也就是执行完 `open` 之后
    - readyState === 2： 表示 `send` 方法已经执行完成
    - readyState === 3： 表示正在解析响应内容
    - readyState === 4： 表示响应内容已经解析完毕，可以在客户端使用了
   xhr.send();
 
 
    4.第四步：利用ajax对象的事件监听第三步是否完成。
   xhr.onreadystatechange = function () {//只要第三步的就绪状态码发生改变，立刻触发此事件。
     if (xhr.readyState === 4) {//表示响应内容已经解析完毕，可以在客户端使用了
        console.log(xhr.responseText);//利用xhr.responseText获取接口里面的数据，返回的一律是字符串格式。
       console.log(JSON.parse(xhr.responseText));//获取数据，格式化成对象
     }
   };

   <script>
  let obj = new XMLHttpRequest()//    1.利用内置的构造函数(XMLHttpRequest)创建ajax对象
  obj.open('get','http://www.baidu.com',true)
  //2.利用ajax对象下面open的get方法打开或者连接通讯的接口
  obj.send()//                        3.利用ajax对象的send方法发送解析
  obj.onreadystatechange=function(){//4.只要状态码发生改变，立刻触发此事件
    if(readyState===4){//             5.表示响应内容已经解析完毕，可以在客户端使用了
      console.log(JSON.parse(obj.responseText));
    } //6.responseText获取数据，因为是字符串格式的，用JSON.parse转为对象
  }
</script> 
 
 
  # 三.ajax四步曲的注意事项
   1.ajax是异步的，异步指的是onreadystatechange。
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'http://localhost:8888/goods/list', true);
   xhr.onreadystatechange = function () {//异步的
     if (xhr.readyState === 4) {
       console.log(JSON.parse(xhr.responseText));
     }
   }
   xhr.send();
 
   2.通过onload方法，获取对应的数据。
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'http://localhost:8888/goods/list', true);
   xhr.send();
   xhr.onload = function () {//onload:xhr加载完成
     console.log(JSON.parse(xhr.responseText));
   }
 
 
   3.同步获取,所谓同步后一个任务等到前一个任务完成，直接无需判断，按照顺序一步一步完成。
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'http://localhost:8888/goods/list', false);
   xhr.send();
   console.log(JSON.parse(xhr.responseText));
</script>

# 四.ajax的渲染
  <style>
    * {
      padding: 0;
      margin: 0;
      list-style: none;
    }
 
    .goodslist {
      width: 1170px;
      margin: 0 auto;
    }
 
    .goodslist li {
      float: left;
      width: 200px;
      padding: 10px;
      height: 300px;
      border: 1px solid #ccc;
      margin: 0 10px 10px 0px;
    }
 
    .goodslist li img {
      width: 200px;
    }
 
    .goodslist li p {
      width: 200px;
      height: 48px;
      line-height: 24px;
      overflow: hidden;
    }
  </style>
</head>
 
<body>
  <div class="goodslist">
    <ul>
      <!-- <li>
        <img src="" alt="">
        <p></p>
        <span></span>
      </li> -->
    </ul>
  </div>
</body>
 
</html>
<script>
  // 一.渲染render
  // 1.获取接口数据 - http://localhost:8888/goods/list
  let obj = new XMLHttpRequest();
  obj.open('get', 'https://www.tianqiapi.com/api?version=v1&appid=21375891&appsecret=fTYv7v5E&city=福州', true);
  obj.send();
  obj.onload = function () {
    // 获取数据,转换成对象
    let arr = JSON.parse(obj.responseText).list;
    console.log(arr);
    // 2.渲染对应的结构
    let str = '';//空字符串
    for (let value of arr) {//拼接
      str += `
        <li>
          <img src="${value.img_big_logo}" alt="">
          <p>${value.title}</p>
          <span>${value.price}</span>
        </li>
      `;
    }
    // 追加
    document.querySelector('.goodslist ul').innerHTML = str;
  };
</script>


# 五.ajax（get）发送数据
      
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


# 六.ajax（post）发送数据
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


# 七.ajax(get和post)的区别
1.语义化：get适合获取，post适合携带数据
2.安全性：get不安全，数据拼接在地址栏的后面，post通过请求头传输
3.长度性：get长度有限，地址栏后仅支持拼接2000多个字符，post理论上没有限制
4.缓冲性：get有缓存的，post没有缓存的

# 携带数据的方式:
          1.get地址栏携带
          2.post请求头配合send携带
