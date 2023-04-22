###  document.write 在浏览器中显示
###  console.log  在控制台显示


# 一. 三目运算符
   // 基本语法: 条件? 语句1: 语句2
    // 三目运算符用来做简单的分支判断
    // 1.三目运算符特点
    // 返回值(将语句结果赋值给某个变量)
    // 嵌套使用
    // 满足条件执行的语句必须是一条语句。

1.案例：输入三个数字，输出其中的最大值（两两比较）。
    // 思路：先比较a和b，再有a和b的最大值去和c比较。
    var a = 12;
    var b = 50;
    var c = 7;
    var max = 0; //接收最大值的变量
    max = a > b ? (a > c ? a : c) : (b > c ? b : c);
    console.log(max);

2.案例：输入三个数字，输出其中的最大值（两两比较）。
  var x=+prompt('请输入数字')
      y=+prompt('请输入数字')
      z=+prompt('请输入数字')
  var max = x>y?(x>z?x:z):(y>z?y:z)
      console.log(max)

# 二.运算符的优先级
    // 1.添加括号，括号的优先级最大。
    // 2.核心关注的几个符号的优先级。
    // () -> [].  ->  !  ->  ==  -> && -> || -> ?:  最后就是赋值(= +=)

# 三.梳理核心内容
    一.if语句
    1.if语句的三种结构
    2.if语句的三个特点
        - else可以省略，else短路操作
        - 将最大的可能给if语句
        - if语句的条件可以是任意的表达式，结果一定是布尔值。
 
    二.switch语句
    1.switch基本结构
    2.switch语句的特点。
        - switch括号里面的值恒等于case后面的某个值，执行case后面对应的语句块。
        - 每一个case都表示一个分支，case具有穿透力，需要给每一个情形后面添加break, break表示switch语句的结束
        - default表示不满足任何一个case而执行的语句块，类似于if语句里面的else，default可以省略
  
    三.if语句和switch语句的区别
    1.switch语句通常处理case为比较确定的值的情况，而if...else...语句更加灵活，常用于范围判断（大于、等于、小于某个范围）；
    2.switch语句进行条件判断时，找到对应的条件直接执行，效率更高。而if...else...语句，有几种条件，就得进行几次判断。
    结论：
    当分支比较少的时候，if...else...语句的执行效率比switch语句高；
    当分支比较多时时候，switch的执行效率高，而且结构清晰。
 
    四.三目运算符
    1.三目的基本的结构
    2.三目的特点。
        - 返回值(将语句结果赋值给某个变量)
        - 嵌套使用
        - 满足条件执行的语句必须是一条语句。

# 三.练习：开发一款软件，根据公式（身高-108）*2=体重，可以有10斤左右的浮动。来观察测试者体重是否合适(身高：cm)
    // 思路
    // 根据结果猜想三种可能：标准身材，偏胖，偏瘦（三种分支）
    // 根据三种分支，设计三种条件。
    // 偏胖  体重 >（身高-108）*2+10
    // 偏瘦  体重 <（身高-108）*2-10
    // 标准  偏瘦 <= 体重 <= 偏胖

  var shengao = prompt("请输入身高");
      tizhong = prompt("请输入体重");
      a = (shengao - 108) * 2 + 10;
      b = (shengao - 108) * 2 - 10;

  if (tizhong > a) {
    console.log("肥胖");
  } 
  else if (tizhong < b) {
    console.log("偏瘦");
  } 
  else if (tizhong <= a && tizhong >= b) {
    console.log("标准");
  } 
  else {
    console.log("输入有误");
  }

# 四..while循环
    // while 语句属于前测试循环语句，也就是说，在循环体内的代码被执行之前， 就会对限制条件求值。因此，循环体内的代码有可能永远不会被执行。
 
    // 注意循环的特点：程序的循环速度非常快，大部分循环需要执行完成，才显示最终的结果。
 
    // 基本结构
    // while(限制条件){ 满足条件执行的循环体(语句块) }
 
    // 案例1：输出1-100
    // var num = 1; //初始值  执行一次
    // while (num <= 100) { //num <= 100 限制条件，大括号里面的是循环体
    //     document.write(num);
    //     num++; //101  当num=101时，num不满足条件，循环结束
    // }
    // console.log(num); //101
 
    // 案例2：利用select渲染1000年
    // document.write('<select>')
    // var year = 1900; //初始值 
    // while (year <= 3000) { //限制条件
    //     //循环体
    //     document.write('<option>' + year + '</option>');
    //     year++;
    // }
    // document.write('</select>')
 
 
    // 案例3：打印100以内能够被7整除的数字。
    // var num = 1;
    // while (num <= 100) {
    //     if (num % 7 === 0) {
    //         document.write(num + ',');
    //     }
    //     num++;
    // }
 
 
    // 二.while循环的嵌套，循环里面还有循环。
    // 外层循环一次，内层的循环全部完成。
    var i = 1;
 
    while (i <= 10) {
        document.write('我是外层循环的第' + i + '<br>');
        i++;
 
        // 嵌套一个10次循环
        var j = 1;
        while (j <= 10) {
            document.write('   我是内层循环的第' + j + '<br>');
            j++;
        }
    }
<body>
    <li>我是li标签</li>
  </body>
</html>
<script>
  var num = 1
  while(num <= 1000){
    num++
    document.write('<li>我是li标签</li>')
    console.log(num)
  }
</script>

# 五..while循环的练习
     案例1：绘制10*10表格(table,tr,td)
   <script>
  document.write('<table width=400px heith=400px border=1 cellspacing="0">')
    var a = 1
    while(a<=10){
      document.write('<tr></tr>')
      a++
      console.log(123,a)
      b=1
      while(b<=10){
        document.write('<th>77777</th>')
        b++
        console.log(145,b)
      }
    }
  document.write('</table>')
</script>
 
    // 案例2：绘制九九乘法表
    // 思路：
    // 1.外层循环一次，内层循环一次，内层循环的次数和外层第几次循环有关系
document.write('<table width=400px height=400px border=1 cellspacing="0">');
  var a = 1;
  while (a <= 9) {
    document.write("<tr></tr>");
    b = 1;
    while (b <= a) {            #############,绘制九九乘法表时,b的循环次数按照a的循环次数
      document.write('<th>' + b + 'x' + a + '=' + b*a + '</th>');
      b++;
      console.log(145, b);
    }
    a++;                        #############，绘制九九乘法表时，a++一定要放在下面，1.放在上面则表示，a循环一次，b就会循环2次，
    console.log(123, a);                                                          2.放在下面则表示，a循环一次，b就会循环（a+b）次             
  }
  document.write("</table>");
</script>

# 六.do...while...
    // 1.do-while 语句是一种后测试循环语句，即只有在循环体中的代码执行之后，才会测试限制条件。换句话说，在对条件表达式求值之前，循环体内的代码至少会被执行一次。
 
    // var num = 1;
    // do {
    //     document.write(num);
    //     num++;
    // } while (num <= 10);
 
 
    // while (num <= 10) {
    //     document.write(num);
    //     num++;
    // }
 
    // 2.区别，do...while...循环体内的代码至少会被执行一次
    // var num = 10;
    // while (num > 10) {
    //     console.log(num);
    // }
 
    // do {
    //     console.log(num);
    // } while (num > 10);

# 七.for 循环

    // for循环可以理解成while循环的紧凑写法。
    // 1.for循环的结构 - 重点
    // for(初始值;限制条件;计数器变量的更新){  满足条件执行的循环语句块  }
    // 初始值：可以是多条语句，中间用逗号隔开，初始值仅执行一次。
    // 限制条件：可以是多条语句，中间用逗号隔开，但是最终以最后一条限制条件的语句作为参考。
    // 计数器变量的更新：可以是多条语句，中间用逗号隔开，变量的累加累减
<script>
1.案例
  for (var a = 1; a <= 10; a++) {
    document.write("<li>我是li标签<li>");
    console.log("li", a);
    for (var b = 1; b <= 10; b++) {
      document.write("<p>我是p标签</p>");
    }
    console.log("p", b);
  }
</script>

2.案例
document.write("<table border=1 cellspacing=0>");
  for (var a = 1; a <= 9; a++) {
    document.write("<tr></tr>");
    console.log("tr", a);
    for (var b = 1; b <= a; b++) {
      document.write('<th>'+ b + 'x' + a + '='+ a*b + '</th>');
    }
    console.log("th", b);
  }
  document.write("<table>");
</script>

3.案例  100内被7整除的数
  for (var a = 1; a<= 100; a++) {
      if(a % 7 === 0){
        console.log(a)
      }
  }
</script>

4.案例,1+2+3+4+.....100 的和
<script>
  for (var a = 1, b=0; a<= 100; a++) {
     b+=a  //b=b+a...
     console.log(b)
  }
</script>

# 八.break和continue关键字介绍
    // 1.break 语句会立即退出整个循环，强制继续执行循环后面的其它语句。
    // 优化循环，清除没有必要的循环。
    // for (var i = 1; i <= 10; i++) {
    //     if (i === 5) {
    //         break;
    //     }
    //     console.log(i);
    // }
 
    // 2.continue 语句代表立即退出循环，但退出的是当前循环继续执行下一次循环。
    // for (var i = 1; i <= 10; i++) {
    //     if (i === 5) {
    //         continue;
    //     }
    //     console.log(i);
    // }

# 九.如果处理错误，先发现错误，找到错误，解决错误。
    // 代码出现错误，立刻结束，错误代码下面的所有代码都不会执行。
    // 1.debug常见错误类型
    // 1.1.引用错误--referenceError:某个变量或者关键字不存在，直接使用。
    // 报错信息格式：ReferenceError: a is not defined
    // console.log(a);
 
    // 1.2.语法错误--syntaxError:编写的代码违背作者约定的语法格式而报错，这种报错vscode编译器会做出反应。
    // var 1a = 10;
 
    // 1.3.类型错误--TypeError：该语法不能这样使用。
    // 123();//TypeError: 123 is not a function
 
 
    // 1.4.范围错误--RangeError：设置的参数不在约定的范围内。
    // number.toFixed(number):数字对象下面的方法，用来截取小数的位数。
    // var num = 3.1415926;
    // console.log(num.toFixed(2)); //3.14
    // console.log(num.toFixed(-1)); //报范围错误
 
    // 二.自定义错误 - 提前了解
    // 通过系统提供的一个Error类来实现，通过new关键字去调用类，产生一个错误对象。
    // 通过throw关键字将错误抛出到浏览器的下面。
    // throw new Error('我错了');

# 十。一.断点  debugger
    // 1.概念：代码执行到断点的地方，停止执行，等待指示。
    // 2.如何添加断点
    // 第一种方式：直接在代码里面添加debugger关键字。
    // 第二种方式：通过控制面板 - sources面板 - 点击代码对于的行号添加断点。
 
    // 注意右侧面板上面的watch选项，监听代码中某个变量值的位置。
    // 通过f10快捷键查看循环的每一步，通过f8快捷键查看每一次循环。
 
    for (var i = 1, sum = 0; i <= 10; i++) {
        //手动添加断点
        debugger;
        sum = sum + i;
    }
    console.log(sum);55

# 十一。
