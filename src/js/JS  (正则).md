# 一 正则：
1. 做表单验证：
2. 利用正则，解决核心算法：
3. 利用正则操作字符串会更快和更秀
4. String :正则表达式
5. RegExp :正则表达式

# 二 .创建正则对象：

1. 正则表达式时一个描述字符规则的对象
2. 字符串进行强大的模式匹配和文本检索与替换
3. 利用自定义规则的操作，控制、预定字符串的使用
4. 可选的--修饰符：
                 i：忽略大小写
                 g: 全局匹配
                 m：多行匹配
                 .match(/\d+/g):获取字符串中的所有数字

5. 利用类创建正则对象：
                    var  n = new RegExp()  // n就是正则对象

# 三. 正则的方法：
1. 正则的规则：可以是变量、字符串
2.  test(str)方法在字符串中查找是否存在的正则表达式并返回布尔值，存在返回 true，不存在返回false  
 
    // var reg = /hello/;
    // var str = 'abchelloabc';
    // console.log(reg.test(str)); //true
    // console.log(reg.test('abhellcoHelloabc')); //false
    // console.log(/hello/i.test('abcHeLloabc')); //true 忽略大小写

# 四 .变量和字符串的格式：
     ----var arr = new RagExp('hallo','i')
     ----var arr = /hallo/i

# 1.获取字符串中所有数字，以字符串的形式打印出来
    var arr = 'sjdjck522fe52f3f26f633333'
    console.log(arr.match(/\d+/g)); //获取字符串中所有数字，以字符串的形式打印出来

# 2.获取字符串中所有字母，以字符串的形式打印出来
    var arr = 'sjdjck522fe52f3f26f633333'
    console.log(arr.match(/[a-z]/g)); //获取字符串中所有字母，以字符串的形式打印出来

# 3.获取字符串中所有中文，以字符串的形式打印出来
    var arr = 'sj非ck522fe52f3f26f63张33'
console.log(arr.match(/[\u4e00-\u9fa5]+/g)); //获取字符串中所有中文，以字符串的形式打印出来






# 五. 可以配合正则使用的字符串方法：
#                                1. match      获取数字、字母、中文
#                                2. replace    替换
#                                3. split      删除数字、字母、中文
#                                4. test(str)  查找是否存在：存在返回 true，不存在返回false
#                                              var arr = 'a1b2中国c3d14e5'
#                                              var brr = /d/
#                                              console.log(brr.test(arr))--brr在arr中查找


   1. match    方法获取匹配的内容，返回数组

#           var arr = 'Ed5fd2dRd2sDsC2'
#           --全局匹配字符串中所有的d，忽略大小写
#           console.log(arr.match(/d/gi)) //(5) ["d", "d", "d", "d", "D"]返回数组

   2. search   来查找匹配的数据，和全局没有关系，查找第一个匹配的位置

   3. replace  替换匹配到的数据：2个数据：
                                      1.代表正则
                                      2.代表用来替换的字符串
#           非常重要： 用来过滤敏感词
#           var arr = '这件衣服是你妈的还是你妹的我猜是你大爷的'
#           console.log(arr.replace(/妈|妹|大爷/gi,'*'))----  /|或/全局忽略大小写，'被替换'
#           这件衣服是你*的还是你*的我猜是你*的

   4. split 拆分成字符串数组
#           var arr = 'a1b2c3d4e5f' 
#           console.log(arr.split(/[0-9]/gi)) //干掉0-9的数字
#           (6) ["a", "b", "c", "d", "e", "f"]

#           var arr = 'a1b2c3d4e5'
#           console.log(arr.split(/[a-z]/gi)) //干掉a-z的字母
#           (6) ["", "1", "2", "3", "14", "5"]

#           var arr = 'a1b2中国c3d14e5'
#           console.log(arr.split(/[\u4e00-\u9fa5]/gi)) //干掉所有的中文
#           (3) ["a1b2", "", "c3d14e5"]


###  六.    // 正则的控制字符
              1.x?:         匹配0个或一个x
              2.[]          表示区间范围
              3.^$          视为恒等匹配一个
              4.^           取反（必须使用在[]内）
              5.+           匹配一个或者多个
              6.*           匹配0个或者多个
              7.()+         至少匹配一个（整体）     +和()+的区别是：()+括号内是一个整体
              8.{}          匹配数量                [0-9]{5,10} : 匹配5-10个数字
#  验证手机号码：----console.log(/^1[3|5|7|8|9][0-9]{9}$/.test('18756371756')) true         
              ^$内的，1开头3、5、7、8、9，任意一个0-9的区间的9位(共有11位，不能多，不能少)

#  验证账号：-console.log(/^[A-Za-z][A-Za-z0-9]{6,12}$/.test('a18756371756')) true         
                ^$内的，英文大小写开头，英文大小数字，的区间的9位(共有13位，最少7位，最多13位)
              9./n          代表换行
              10.  .（点）  代表任意字符




#    一.x?:匹配0个或一个人x
        console.log(/a?/.test('bcd')); //true  0个
        console.log(/a?/.test('abcd')); //true  1个
        console.log(/a?/.test('bcd')); //true  0个
        console.log(/a?/.test('aabcd')); //true  2个,因为没有限制

    // 一.中括号 - [] - 表示区间范围，一个中括号对应一个字符。
    // 1.[0-9] 数字0-9中的一个。
    // var reg = /[0-9][0-9]/;
    // console.log(reg.test('abc1abc')); //false
    // console.log(reg.test('abc1ab4c')); //false
    // console.log(reg.test('abc14abc')); //true
 
    // 2.[a-z] 小写字母a-z中的一个
    // 3.[0-9a-z] 数字和小写字母中的一个
    // 4.[0-9a-zA-Z] 数字和字母中的一个
    // 5.[0-4] 数字0-4中的一个
    // 6.[135] 数字135中的一个
 
    // 二.中括号内部的前面添加一个^符号，表示取反
    // 1.[^0-9] 除了数字0-9之外的任何一个字符。
    // console.log(/[^0-9]/.test('1')); //false
    // console.log(/[^0-9]/.test('1a')); //true
    // 2.[^0-9a-zA-Z] 除了数字字母之外的任何一个字符。
 
    // 三.首尾匹配
    // 如果正则表达式的前后添加一个^和$符号，视为恒等匹配。
    // ^ 行首匹配
    // $ 行尾匹配
       console.log(/^a?$/.test('a'))//true
       console.log(/^a?$/.test(''))//true
       console.log(/^a?$/.test('aa'))//false
       console.log(/^a?$/.test('b'))//false

    // console.log(/^[^0-9]$/.test('1112641456')); //false  匹配一个字符，而且这个字符是非数字
    // console.log(/^[^0-9]$/.test('a')); //true
    // console.log(/^hello$/.test('hellohellohello')); //false
    // console.log(/^hello$/.test('hello')); //true
 
    // 四.大括号 - {} - 匹配数量
    // [0-9]{5} : 匹配5个数字
    // [0-9]{5,} : 匹配至少5个数字
    // [0-9]{5,10} : 匹配5-10个数字
 
    // console.log(/^abc{5,10}$/.test('abc')); //false
    // console.log(/^abc{5,10}$/.test('abccccc')); //true
    // console.log(/^abc{5,10}$/.test('abcccccc')); //true
    // console.log(/^abc{5,10}$/.test('abcccccccccccc')); //false
 
#    // 五.括号 ()+ 整体--至少匹配一个
    // console.log(/^(abc){5,10}$/.test('abcccccc')); //false 匹配5-10个abc
    // console.log(/^(abc){5,10}$/.test('abcabcabcabcabc')); //true 
 
 
#    // 六.加号+ ：匹配一个或者多个
      var reg = /a+/
      var str = 'aabcc'
      console.log(reg.test(str))//true

    // console.log(/^[a-z]+$/.test('a')); //true 匹配一个或者多个小写字母
    // console.log(/^[a-z]+$/.test('abc')); //true
    // console.log(/^[a-z]+$/.test('abcd')); //true
    // console.log(/^[a-z]+$/.test('abcd123')); //false
 
 
  # // 七.星号* ：匹配0个或者多个
      var reg = /a*/
      var str = 'aabcc'
      console.log(reg.test(str))//true

    // console.log(/^[a-z]*$/.test('')); //true
    // console.log(/^[a-z]*$/.test('1')); //false
    // console.log(/^[a-z]*$/.test('A')); //false
    // console.log(/^[a-z]*$/i.test('Adsafadsfadsf')); //true
 
    // 八.问号? ：匹配0个或者1个
    // console.log(/^[a-z]?$/.test('')); //true
    // console.log(/^[a-z]?$/.test('a')); //true
    // console.log(/^[a-z]?$/.test('ab')); //false
 
 
    // 九.或符号| ：表示或者的意思，匹配其中的字符构成的任意组合。
    // console.log(/^[a|b|c]$/.test('a'));
    // console.log(/^[a|b|c]$/.test('b'));
    // console.log(/^[a|b|c]$/.test('c'));
 
    // 案例：敏感词过滤
    // var str = '"这件衣服是你妈的，还是你妹的，我猜是你大爷的"，你这句话说的真他妈的好';
    // var reg = /妈|妹|大爷|他/g;
    // console.log(str.replace(reg, '*'));
 
    // 案例：匹配手机号码
    // 规则：手机号码11位，第一位是1  第二位358 后面9位任意数字
    // var reg = /^1[358][0-9]{9}$/
    // console.log(reg.test('13312341234')); //true
    // console.log(reg.test('15312341234')); //true
    // console.log(reg.test('153123412344')); //false
    // console.log(reg.test('1531234123')); //false
    // console.log(reg.test('16312341234')); //false
    // console.log(reg.test('17312341234')); //false
    let arr = ["a", "b", "c", "d", "e", "f",
        1, 2, 3, 4, 5, 6, 7, 8, 9, 0
    ]
    let str = "";
    for (let i = 0; i < 4; i++) {
        str += arr[parseInt(Math.random() * arr.length)];
    };
    console.log(str);
</script>

###   七.转义字符
     简单来说就是在一些字符前加 “\” 使它具有其他意义,例如：\d \D \w \W \s \S 
     如果在一个正常字符前添加反斜杠， JavaScript会忽略该反斜杠, 就不再对其做特殊处理， 而是当做普通字符打印使用。
 
 
     1.\d 匹配数字,相当于[0-9]。
     var reg1 = /^[0-9]$/;
     var reg2 = /^\d$/;
     console.log(reg1.test('1'));
     console.log(reg2.test('1'));
     2.\D 匹配非数字， 同[^0-9]相同
     3.\w 匹配字母数字及_   相当于[a-zA-Z0-9_] 
     4.\W 匹配非字母数字及_  相当于[^a-zA-Z0-9_]
 
     5.\s 匹配空白字符、空格、制表符和换行符
     var str = '  abc  def  ';
     console.log(str);
     console.log(str.replace(/\s+/g, '')); //将一个或者对个空格替换成空。
     6.\S 匹配非空白字符,空格.
 
     7.\n 匹配换行符
     console.log('abcdefg');
     console.log('abcd\nefg'); //字符串中可以插入这样的符号进行换行。
 
 
     8.点符号：匹配除换行符\n外的任意字符
 
     var reg = /^.$/;
     console.log(reg.test('a')); //true
     console.log(reg.test('#')); //true
     console.log(reg.test('\n')); //false
     console.log(reg.test('1')); //true
 
     如果就想匹配真正的点符号。
     var reg = /^.com$/;  //不是点，是任意字符
     var reg = /^\.com$/; //不是点，是任意字符
     console.log(reg.test('.com')); //仅仅匹配.com，其他都不行
 
 
     var reg1 = /^d$/; //匹配d字母
     var reg2 = /^\d$/; //匹配数字
     var reg3 = /\\/; //匹配一个反斜杠



# 案例1. 用正则方法：验证账号密码：----账号英文字母开头，密码纯数字

<style>
  .father {
    width: 400px;
    height: 400px;
    margin: 0 auto;
  }
  span{
    color: red;
  }
  p {
      opacity: 0;
      color: red;
  }
  .span2,.span4{
    opacity: 0;
    color: red;
  }
</style>
<body>
  <div class="father">
    <input value="">
    <span>*</span>
    <span class="span2">账号输入错误</span>
    <p>请重新输入账号</p>
    <input value="">
    <span>*</span>
    <span class="span4">密码输入错误</span>
    <p>请重新输入密码</p>
    <button>验证</button>
  </div>
</body>
</html>
</html>
<script>
  var father = document.querySelector('.father')    
  var input = document.querySelectorAll('input')    1.获取input数组
  var button = document.querySelector('button')     
  var span = document.querySelectorAll('span')      2.获取span数组
  var p = document.querySelectorAll('p')            3.获取p数组
  input[0].focus()                                  4.给第一个input获得光标
  button.onclick = function(){ 
    if(input[0].value !==''){                       5.如果账号的input的value值为空
      if(input[0].value = /^[A-Za-z][A-Za-z0-9]{6,12}$/.test(input[0].value)){
        7.如果账号的input的value值 = 正则的规则，检查：账号的input的value值
        span[0].style.color = '#000'                8.span[0]的颜色为黑色
      }else{
        span[1].style.opacity= 1                    9.否则，第二个span出现
        input[0].value =''                          10.第一个inputvalue值清空
      }
    }else{                                          
      p[0].style.opacity= 1                         6.否则，第一个p标签出现
    }
    if(input[1].value !==''){
      if(input[1].value = /^[A-Za-z0-9]{6,12}$/.test(input[1].value)){
        span[2].style.color = '#000'
      }else{
        span[3].style.opacity= 1
        input[1].value =''
      }
    }else{
      p[1].style.opacity= '1'
    }
  } 


##### 一.案例2，将地址栏数据对象的某些提取出来 

2. eval()
         ----将字符串格式的对象转为对象
#       var arr = 'https://www.baidu.com?a=1&b=2&c=3&d=4'
                  
#       arr = arr.substring(arr.indexOf('?')+1)
                 substring截取字符串,从?开始到结束，+1代表向后一位 

#       console.log(arr)  //    a=1&b=2&c=3&d=4
           
#       console.log(eval('({'+arr.replace(/&/g,',').replace(/=/g,':')+'})'));
                    正则（） { 'arr内替换    &为，      替换    =为：   }








#   一.正则的分组 - ()
    // 1.捕获性分组：把每个分组里匹配的值保存下来
    // var reg1 = /^([a-z])([a-z])([a-z])$/;
    // var str1 = 'abc';
    // console.log(str1.match(reg1)); //['abc', 'a', 'b', 'c']
    var arr = [str1.match(reg1)];
    console.log(arr);
 
    // 2.非捕获性分组：分组内部的前面添加?:,每个分组里匹配的值不会保存下来
    // var reg2 = /^(?:[a-z])(?:[a-z])(?:[a-z])$/;
    // var str2 = 'abc';
    // console.log(str2.match(reg2)); //['abc']
    // 注意： 全局下面，结果是一样的。
 
 
    // 二.分组的应用
    // 1.正则的分组  \1 \2......
    // \1表示和第一个分组配置的值相同。
    // \2表示和第二个分组配置的值相同。
    // \3表示和第三个分组配置的值相同。
    // ....
    // var reg1 = /^([a-z])([a-z])([a-z])\1\2\3$/;
    // console.log(reg1.test('abcabc')); //true
    // console.log(reg1.test('fghfgh')); //true
    // console.log(reg1.test('acbabc')); //false
    // console.log(reg1.test('acbacb')); //true
 
    // 案例：
    // var str = '我我喜欢大家好好学习，天天向上';
    // var reg = /([\u4e00-\u9fa5])\1/g;
    // console.log(str.match(reg)); //['我我', '好好', '天天']
 
 
    // var str1 = '我要一心一意的，我要十全十美，我不能这样不三不四';
    // var reg1 = /([\u4e00-\u9fa5])[\u4e00-\u9fa5]\1[\u4e00-\u9fa5]/g;
    // console.log(str1.match(reg1));
 
 
    // var str2 = '安安静静';
    // var reg2 = /([\u4e00-\u9fa5])\1([\u4e00-\u9fa5])\2/g;
    // console.log(str2.match(reg2)); //注意：?:和\1\2这些不能同时存在。
 
    // 利用属性获取对应的值
    // console.log(RegExp.$1); //获取第一个分组匹配的值
    // console.log(RegExp.$2); //获取第二个分组匹配的值
