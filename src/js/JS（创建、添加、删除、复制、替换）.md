# 十，创建、添加、删除、克隆、替换
1.创建元素对象：
 document.createElemrnt('元素对象的名称')
 var aImg = document.createElemrnt('img')
 console.log(aImg)

2.也可以给创建的元素添加属性：
aImg.src = '../'  ----添加哪一张的图片
aImg.className = 'yi' ---起class名
aImg.style.border = '1px solid red'

3.追加元素对象：将创建好的元素追加到某个元素内部的后面
父元素.appendChild(创建的子元素)
var a = document.querySelector(".box");
 document.body.a.appendChild(cImg)---将创建好的img元素追加到body内部的最下面

4.插入元素对象：将创建好的元素追加到某个元素内部的前面
父元素.insertBefore(父元素)
var box = document.querySelector('.box')--必须先获取父元素
 document.body.insertBefore(cImg，box)---将创建好的img元素放前面，获取的父元素变量放后面

5.删除子元素：removeChild  ---将创建好的元素删除
var box = document.querySelector('.box')--必须先获取父元素
 document.body.removeChild(box)---删除父元素内部的所有子元素

# 如：删除父元素内的某一个子元素
  <body>
    <div class='box'>
      <img src="../img/女好骚.png" alt="" />
      <span>距离下线时间只剩100秒</span>
    </div>
  </body>
</html>
<script>
var a = document.querySelector(".box");   1.先获取父元素
var b = document.querySelector("span");   2.再获取父元素内的所有子元素
document.body.a.removeChild(b)
console.log(a)
</script>

# 如：删除父元素内的相同的某一个子元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
var a = document.querySelector('ul')         1.先获取父元素
var b = document.querySelectorAll('ul li')   2.再获取父元素内的所有子元素
for (i=0;i<b.length;i++){                    3.利用循环遍历所有的子元素
  b[i].onclick = function(){                 4.点击子元素的内容时
    a.removeChild(this)                      5.父元素（this指向谁时，删除谁）
  }
}
</script>

# 如：复制或克隆元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
  var a = document.querySelector("ul");  1.先获取要复制的元素
  var b = a.cloneNode()                  2.如果只要复制这个元素本身的话，（）内不加内容
  var b = a.cloneNode(true)              3.如果要复制这个元素本身以及内部的所有元素，（）内加true或非0的数字
  document.body.appendChild(b)           4.追加到body（父元素）内的最后面----如果父元素不是body，则要先获取父元素
</script>

# 如：替换元素
      ---父元素.replaceChild（添加的元素，被替换的元素）
      将ul元素替换成p元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
  var b = document.createElement("p");                    1.先创建一个p元素
  var a = document.querySelector("ul");                   2.获取被替换的ul元素
  b.style='width:20px;height:20px;border:1px red solid'   3.设置创建的p元素的css属性
  document.body.replaceChild(b,a)                         4.父元素.replaceChild（创建的元素，被替换的元素）
</script>                                                    ----如果父元素是自己设置的，则var获取父元素        

# 如 如果只想替换元素，而内容不变则
      ---父元素.replaceChild（添加的元素，被替换的元素）
      将ul元素替换成p元素
  <body>
    <ul>
      <li>1111</li>
      <li>2222</li>
      <li>3333</li>
      <li>4444</li>
    </ul>
  </body>
</html>
<script>
  var b = document.createElement("p");             1.先创建一个p元素
  var a = document.querySelector("ul");            2.获取被替换的ul元素
  b.innerHTML=a.innerHTML                          3.将p内的内容替换成ul的内容
  document.body.replaceChild(b,a)                  4.父元素.replaceChild（创建的元素，被替换的元素）
</script>  



### 微博发布案例：
  <style>
    textarea {
      width: 600px;
      height: 150px;
      border: 2px red solid;
      margin-bottom: 10px;
    }
    button {
      margin-bottom: 10px;
    }
    .father {
      display: flex;
      width: 600px;
      height: 150px;
    }
    ul li a {
      color: brown;
    }
  </style>     document.onkeydown = function(){} 按下ctrl和回车发送消息
  <body>       if(ev.ctrlKey && ev.which ===13)
    <textarea name="" id="" cols="40" rows="80"></textarea>     1.设置文本框标签
    <br />
    <button>微博发布按钮</button>
    <div class="father">
      <span>你发布了：</span>
      <ul></ul>           7.ul标签内部设置li标签，当文本框发布内容时，创建一个li标签
    </div>
  </body>
</html>
<script>
  var oTextarea = document.querySelector("textarea");
  var oButton = document.querySelector("button");
  var oUl = document.querySelector("ul");
  oTextarea.focus();                                 2.文本框自动获取光标  
  oButton.onclick = function () {                    3.点击发布按钮时
  var Time = new Date();                             4.获取当前时间（放在点击事件内，实现什么时候点击，发布就是什么时候）
    if (oTextarea.value !== "") {                    5.当文本框的内容不等于空时
      var oLi = document.createElement("li");        6.创建一个li标签
      oLi.innerHTML =                                8.li标签的文本内容
      oTextarea.value                                  文本框的内容
      +'<a href="javascript:;">删除</a>'               +一个a标签的删除按钮
      + "<br>"                                        +换行
      + Time.toLocaleString();                        +获取的当前时间
      if (oUl.children.length >= 1) {                9.如果ul的所有子元素索引长度大于等于1）时
        oUl.insertBefore(oLi, oUl.children[0]);      10.将最近创建好的li放在ul的无空格最前面
        if(oUl.children.length>=4){                  15.如果ul的所有子元素索引长度大于4时，
          oUl.removeChild(oUl.lastElementChild)      16.则删除ul内的最后一个li标签
        }
      } else {
        oUl.appendChild(oLi);                        11.否则，ul如果没有任何内容时，则把当前创建好的li标签放入到ul内
      }
      oTextarea.value = "";                          13.文本框的内容为空
    } else {
      alert("请输入内容");                            14.如果当文本框的内容等于空时，点击发布按钮，alert显示为"请输入内容"
    }
    var oA = document.querySelector("ul li a");      17.获取a
    oA.onclick = function () {                       18.点击a时，
      if (window.confirm("你确定要删除吗?")) {        19.window的删除按钮
        oUl.removeChild(this.parentNode);            20.删除ul的（点击谁，则调用谁。的父元素）
      }
    };
  };
</script>
  function fx(ev){                             或者:用事件委托的方式来获取a元素
    var ev=ev||event
    if(ev.target.nodeName ==='A' ){           如果ul的子元素（孙元素也可以）的元素名称==='A'时
      ul.removeChild(ev.target.parentNode)     删除父元素的（子元素的.父元素）
    }
   }
   ul.addEventListener('click',fx,false)       点击父元素（事件委托一定要找到父元素）