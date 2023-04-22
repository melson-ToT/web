  # 一.JSONP实现跨域
   JSONP:JSON with Padding，利用json数据进行填充(将JSON数据填充给函数，利用函数的传参获取)
   1.script标签的src属性不存在跨域，可以引入本地或者第三方的文件内容。
   2.JSONP仅支持get请求，这也是JSONP的弊端，通过地址栏获取或者修改函数名称。
   3.函数名称是前后端借助回调函数实现的(如何制作JSONP接口)
</script>
 
<!-- 利用script获取本地的数据 -->
<!-- <script src="demo.js"></script>
<script>
  console.log(arr);//'zhangsan', 'lisi', 'wangwu']
</script> -->
 
<!-- 利用script获取第三方的数据 -->
<!-- 
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.6.3/jquery.js"></script>
<script>
  console.log($);
</script> -->
 
 
<!-- JSONP获取数据 -->
<script>
  function fn(arr) {
    console.log(arr);//['zhangsan', 'lisi', 'wangwu', 'hehe']
  }
</script>达斯官网正品旗舰店","15166.377880184331"],["aape羽绒服","8699.985968699406"],["aaxin","9346.609528257823"],["aaad","5483.910681399631"],["啊阿迪达斯官网正品旗舰店男鞋","1
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



  # 二.JSONP的特点
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
