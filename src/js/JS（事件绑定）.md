# 一.事件绑定：
    1.事件绑定为true:从大到小      ---事件绑定的优先级大于冒泡
    2.冒泡为false；从小到大

1.普通事件，如果出现相同的时间，后面的会覆盖前面的
2.DOM 0 级事件，一个元素对象只能绑定一个事件处理函数（相同类型的事件）否则会出现覆盖 3.取消普通事件：
document.onclick = null

4.事件绑定、事件监听、事件侦听：
DOM 2 级事件：事件类型相同的情况下，一个元素对象上面只能绑定多个事件处理函数，按顺序执行
标准：--元素对象.addEventListener() 增加事件监听
非标准：--attachEvent()

# 二.addEventListener(事件类型、事件处理函数、是否捕捉)

----事件类型:没有 on，直接使用：click、mouseout、mousedoen、keyup....
----事件处理函数：函数给对象
----是否捕捉：参数可以省略，默认：false(冒泡)；true（捕捉）

# 案例：事件写法：  区别事件是否是冒泡还是捕捉
  <body>
    <div>中国人民</div>
  </body>
</html>
<script>
  var div = document.querySelector("div");
  div.addEventListr('click',fn,false)
  function fn(){
    div.style.backgroundColor = "red";
  }
  // div.addEventListr('click',fn,false)为：冒泡
  // div.addEventListr('click',fn,true)为：捕捉
</script>

# 三.取消事件绑定：
            ----removeEventListener(事件类型、事件处理函数、是否捕捉)

1. 注意移出事件绑定的参数和添加事件绑定的参数是一致的
2. 标准：removeEventListener(事件类型、事件处理函数、是否捕捉)
3. 非标准：datechEvent(事件类型、事件处理函数)

### 案例：鼠标移入时监听，移出时，取消绑定
  <body>
    <input type="text" value="请输入内容" />
    <div>中国人民</div>
  </body>
</html>
<script>
  var input = document.querySelector("input");
  var div = document.querySelector("div");
  input.addEventListener("click", fn, false);
  function fn() {
    input.value = div.innerHTML;
    div.style.display = "block";
  }
  input.onblur = function () {
    div.style.display = "none";
    input.removeEventListener("click", fn, false);
  };
</script>