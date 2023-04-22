
   一.跨域和同源策略
   1.获取第三方接口(其他公司的，不是本公司后端)的时候出现一个错误情况
   淘宝搜索的第三方接口：https:suggest.taobao.com/sug?k=1&area=c2c&q=a&code=utf-8&ts=1672293708041

   <script>
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'https:suggest.taobao.com/sug?k=1&area=c2c&q=a&code=utf-8&ts=1672293708041', true);
   xhr.send();
   xhr.onload = function () {
     console.log(xhr.responseText);报错了，错误中包含下面的信息 No 'Access-Control-Allow-Origin'
   }
   上面的错误，叫做跨域错误。
    </script>
 
   2.为什么产生跨域错误
   因为浏览器为了自身的安全，提出一个[同源策略]的思想。
 
   3.同源策略
   阻止从一个域名上加载的脚本获取或操作另一个域名上的文档属性(数据)。
   也就是说，受到请求的URL的域必须与当前Web页面的域相同。
   同源策略是浏览器最核心也最基本的安全功能，如果缺少了同源策略，则浏览器的正常功能可能都会受到影响。
 
 
   二.什么情况会产生跨域
   1.域名不同必须产生跨域
   2.协议不同产生跨域  http和https
   3.端口不同产生跨域
   4.域名和域名对应的ip地址都会产生跨域，  localhost和127.0.0.1
   5.一级域名和二级域名产生跨域
   ...
 
   例如
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'http://localhost/JS2214/week06/DAY29/code/demo.php', true);
   xhr.send();
   xhr.onload = function () {
     console.log(xhr.responseText);
   }
 



# 二.解决跨域的方式
   1.后端代理：后端不存在跨域(后端脱离浏览器)
   当前的接口是本公司的后端设计的，所有不存在跨域访问
   如果前端获取第三方接口出现跨域，委托本公司的后端帮忙获取，然后给前端。
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'http://localhost/JS2214/week06/DAY29/code/demo.php', true);
   xhr.send();
   xhr.onload = function () {
     console.log(xhr.responseText);
   }
 
   2.跨域资源共享（CORS）
   如果本公司的后端提供的接口因为安全问题产生了跨域，请求后端将跨域访问的域名添加到对应的接口里面，也能够解决跨越。
   let xhr = new XMLHttpRequest();
   xhr.open('get', 'http://127.0.0.1/JS2214/week06/DAY29/code/demo.php', true);
   xhr.send();
   xhr.onload = function () {
     console.log(xhr.responseText);
   }
 
 
  // 3.JSONP:前端的解决跨域的核心
  // 如果第三方接口是JSONP格式，无需后端，前端独立完成的(注意：制作JSONP格式的接口必须前后端一起)



# 三.JSONP实现跨域
   JSONP:JSON with Padding，利用json数据进行填充(将JSON数据填充给函数，利用函数的传参获取)
   1.script标签的src属性不存在跨域，可以引入本地或者第三方的文件内容。
   2.JSONP仅支持get请求，这也是JSONP的弊端，通过地址栏获取或者修改函数名称。
   3.函数名称是前后端借助回调函数实现的(如何制作JSONP接口)
</script>
 


(一).利用script中，数组或对象类型获取本地的数据
1.
<script src="lianxi.js"></script>  //constconst arr = ['zhansan','lisi','wangwu']
<script>
console.log(arr);//['zhansan','lisi','wangwu']
</script>

 
2.
<script src="lianxi.js"></script>  //const obj ={name:'zhangsan',age:'男',sex:20} 
<script>
console.log(obj);//{name:'zhangsan',age:'男',sex:20} 
</script>
 
 
3. 通过JSONP获取：函数传参
                (1).js文件中，参数必须双引号  //fn(["zhansan","lisi","wangwu"])
                (2).将<script>中的形参带入
                (3).js文件，放在<script>的下面,因为先有函数，再有函数调用
<script>
  function fn(arr){
    console.log(arr);// ["zhansan", "lisi", "wangwu"]
  }
</script>
  <script src="lianxi.js"></script>



</script>
[达斯官网正品旗舰店","15166.377880184331"],["aape羽绒服","8699.985968699406"],["aaxin","9346.609528257823"],["aaad","5483.910681399631"],["啊阿迪达斯官网正品旗舰店男鞋","1]
</script>
<script src="demo.txt"></script>
<!-- fn(["zhangsan", "lisi", "wangwu","hehe"]) -->
 
 
<!-- JSONP获取数据 -->
<script>
  function taobao(res) {
    console.log(res);
  }
</script>
<script src="https://suggest.taobao.com/sug?k=1&area=c2c&q=aa&code=utf-8&ts=1672293708041&callback=taobao"></script>
<!-- 
  taobao({"result":[["aape","11190.862248696947"],["aaaaxbbb","8058.711241139813"],["啊阿迪达斯男鞋","49519.03711340206"],["aape卫衣","13612.146388888888"],["aape外套","10468.290746268656"],["啊阿迪8588.991299897647"]]})
 -->
 
<script>
  function nowapi(res) {
    console.log(res);
  }
</script>
 
<script
  src="http://api.k780.com/?app=life.postcode&postcode=528400&appkey=61672&sign=dea8e50c3c5a60e17e91fb06fa1fcd3a&format=json&jsoncallback=nowapi"></script>



  # 四.JSONP的特点
   1.script标签的src属性不存在跨域，可以引入本地或者第三方的文件内容。
   2.JSONP的仅支持get方法，这也是JSONP的弊端，允许前端修改函数名称，通过函数获取对应的JSONP格式的数据
   3.回调函数，描述JSONP格式的制作过程
   过程：前端通过get方式将函数名称放到地址栏上面，后端获取地址栏上面的函数名称，后端拿到数据库里面的数据将其填充到函数调用里面，将整个结构输出为JSONP格式。
 
   注意：如果第三方接口是JSONP格式，无需后端协助，否则都需要后端协助，包括制作JSONP接口也是后端协助。
 
   二.制作淘宝的搜索引擎
   1.分析淘宝搜素引擎接口
   https://suggest.taobao.com/sug?k=1&area=c2c&q=aa&code=utf-8&ts=1672293708041&callback=taobao
   接口地址后面拼接了很多的数据
   名称为q的字段，后面的值就是搜索的内容。
   名称为callback的字段，后面的值就是约定的函数名称
 
   2.制作布局
 
   3.编写代码
   触发input事件，需要创建script标签，因为script的src属性的值是改变的
   <script>
  function taobao(res) {
    console.log(res.result);
     开始渲染数据
    let str = '';
    for (let value of res.result) {
      str += `
        <li>${value[0]}</li>
      `;
    }
    list.innerHTML = str;
  }
 
  search.oninput = function () {
    let jsonp = document.querySelector('#jsonp');//首先获取script
    if (jsonp) {//存在，删除
      jsonp.remove();
    }
    let cScript = document.createElement('script');
    cScript.src = 'https://suggest.taobao.com/sug?k=1&area=c2c&q=' + this.value + '&code=utf-8&ts=1672293708041&callback=taobao';
    cScript.id = 'jsonp';//给script标签添加一个id选择器，方便删除使用
    document.body.appendChild(cScript);
  };
</script>

