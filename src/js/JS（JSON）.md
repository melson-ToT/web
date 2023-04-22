# 一.前段的核心工作
1. 渲染：根据数据渲染对应的html的结构
2. 用户体验
3. 性能优化

# 二.浏览器提供的格式化JSON的插件
安装方法：浏览器三个点>更多工具>扩展程序>开发者模式>加载以解压的扩展程序>选择对应的版本

# 三.JSON对象的介绍：
                ----JSON是最好的前后端交互方式
  1.--JSON的特点：
                JSON的组成：反引号+简单值+'对象'+'数组'
                JSON里面字符串需要添加双引号
                JSON没有var、分号、注释等JS相关的语法

  2.--JSON的静态方法：----非常重要：
                JSON.parse()      :用于从一个字符串中解析出JSON对象，具有检测功能
                                   用于将字符串转为对象

                JSON.stringify()  :将对象转换成JSON格式的字符串


# 案例1：
      ----利用JSON的.parse()方法，将后端的数据进行处理
<script>
 let arr = `["zhangshan","lisi","wangwu","laoliu"]`
 console.log(JSON.parse(arr))//(4) ["zhangshan", "lisi", "wangwu", "laoliu"]
</script> 


# 案例2
  var arr = '["zhangshan","lisi","wangwu","laoliu"]'  1.后端给的JSON
  var brr = JSON.parse(arr)           2.利用JSON的.parse()方法，转换为字符串
  var str = ''                        3.建立一个空数组或对象
  brr.forEach(function (value){       4.循环brr的value值
     str += '<li>'+ value +'</li>'    5.str的每一项 = 每一个li标签内，brr的value值
  })
  document.body.innerHTML = str       6.body的内容 = str
</script>

# 案例3；   将对象转换成JSON格式的字符串 
var arr = {
    a : 1,
    b : 2,
    c : 3 
  }
  var brr = JSON.stringify(arr)
  console.log(brr)           // {"a":1,"b":2,"c":3}

# 注意：对象如果进行传输或者存储，一定要将对象转为字符串格式的存在，数组则可以省略