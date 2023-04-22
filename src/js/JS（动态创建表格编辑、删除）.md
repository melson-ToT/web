# 一 动态创建表格的编辑、删除
1. 根据表单输入的数字创建对应的表格
   --table使用innerHTML时候会默认生成tbody标签
   --表单的值是input
</style>
<body>
  <div class="father">
    行: <input type="text"> <br>
    列: <input type="text"> <br>
    <button>编辑表单</button>
  </div>
  <div class="son"></div>
</body>
</html>
</html>
<script>
var input = document.querySelectorAll('.father input')
var button = document.querySelector('button')
var son = document.querySelector('.son')
button.addEventListener('click',fn,false)
function fn (ev){
  var ev = ev || event
  var table = document.createElement('table')    1.创建一个表单
  table.border = 1                               2.边框为1px
  son.appendChild(table)                         3.追加到son
  for(i=0;i<input[0].value;i++){                 4.循环第一个input的值
    var tr = document.createElement('tr')        5.创建行
    table.appendChild(tr)                        6.追加到表单里
    for(j=0;j<input[1].value;j++){               7.循环第二个input的值
      var td = document.createElement('td')      8.创建列
      tr.appendChild(td)                         9.追加到行里 
      if(j===input[1].value-1){                  15.如果最后一个列
      td.innerHTML='<a href="javascript:;">删除'+i+'</a>'16.列的内容=a的删除标签+tr的索引
       }
      else{
      td.innerHTML = 111}                         10.列的内容是111
    }
  }
}
son.addEventListener('dblclick',fx,false)        11.点击父元素时（利用事件委托）
function fx(ev){
  var ev = ev || event
  if(ev.target.nodeName === 'TD'){               12.当需要的子元素的元素名称===元素名称TD
    ev.target.innerHTML = '<input value="'+ev.target.innerHTML+'">'
    13.子元素的内容=input内之前的子元素的内容
    ev.target.children[0].addEventListener('blur',fs,false)
    14.当input的第一个子元素失去焦点时
    function fs(){
      this.outerHTML=this.value   15.input本身=input的value值
    } 
  }else if(ev.target.nodeName === 'A'){          17.当需要的子元素的元素名称===元素名称A
    ev.target.parentNode.parentNode.parentNode.removeChild(ev.target.parentNode.parentNode)
  }  18.A元素的父元素的父元素的父元素.删除（A元素的父元素的父元素）
}                   tbody(tr)父元素必须比子元素大一级
</script>





