#  // 程序的三大结构
    // 1.顺序结构
    // 开发中编写的代码按照顺序执行，从上到下，从左到右的顺序执行，遇到错误，立刻终止，代码结束。
    // console.log(1);
    // console.log(2);
    // console.log(我错了);
    // console.log(3);
    // console.log(4);
    // console.log(5);
 
 
    // 2.选择结构
    // 选择结构表示代码执行过程中出现了条件选择(分支)，根据设定的条件确定选择那个分支执行。
    // 选择结构有单选择、双选择和多选择三种形式。
    // 2.1.if语句
    // 2.2.switch语句
    // 2.3.三目运算符
 
 
    // 3.循环结构
    // 循环结构表示程序反复执行某个或某些操作，直到某条件为假（或为真）时才可终止循环。
    // 2.1.while
    // 2.2.do...while...
    // 2.3.for

# 一.语句和语句块
    // 1.语句：一个语法上自成体系的单位，它由一个词或句法上有关连的一组词构成 - 了解
    // var a = 1;  break;
    // 2.语句块
    // 程序中由{}包含的一条或者多条语句称之为语句块。
    // {
    //     var a = 1;
    //     var b = 2;
    //     console.log(a + b);
    // }
 
    // 3.分号
    // js语句后面的分号是可选的，表示语句结束，如果一行表示一条语句，可以省略分号。
    // 如果添加分号，每一条语句都添加，否则都不添加。
    // var a = 1;
    // var b = 2;
    // console.log(a + b);
 
    // 4.注意
    // 如果语句块里面只有一行代码，在很多场景下可以省略{}

# 二.选择结构 - if语句
    // 1.if的三种基本结构(基本语法：作者约定的格式)
    // if的条件可以是任意的表达式，ES会自动调用Boolean()转换函数将这个表达式的结果转换为一个布尔值。
    // 操作数为假的情况：0 '' null undefined NaN false 其他的都是为真。
 
    // 1.1.单分支:只有一种选择
    // if (条件) {满足条件执行的语句块}
    // if (1 + 1) {
    //     console.log('if条件满足，执行此代码1');
    // }
    // if (0) {
    //     console.log('if条件满足，执行此代码2');
    // }
 
    // 例子：输入数字判断
    // var num = prompt('请输入一个数字');
    // if (!isNaN(num)) { //判断是数字的条件，因为取反了
    //     console.log('是数字');
    // }
 
 
    // 1.2.双分支：两种选择
    /* 
    格式：
    if (条件) {
        满足条件执行的语句块
    } else {
        不满足条件执行的语句块
    } 
    */
 
    // var num = prompt('请输入一个数字');
    // if (!isNaN(num)) { //判断是数字的条件，因为取反了。
    //     console.log('是数字');
    // } else { //不是数字
    //     console.log('不是数字');
    // }
 
    // 重点注意：else短路操作,满足if语句，执行if语句，执行完即结束。
    // var num = prompt('请输入一个数字');
    // if (!isNaN(num)) { //判断是数字的条件，因为取反了。
    //     console.log('是数字');
    // } else { //不是数字
    //     fasdfjdsalkfjkdas
    //     dsajfldasjflds
    //     adsjfladsjfl
    //     adsjfladsjlkf
    // }
 
    // 案例：输入年份，计算某一年是否是闰年（闰年能被4整除且不能被100整除，或能被400整除）；
    // var year = prompt('请输入四位的年份');
    // 1.先判断是否是数字
    // if (!isNaN(year)) { //是数字
 
    // 2.判断是四位的数字
    //     if (year >= 1000 && year <= 9999) { //是四位数 不允许这样操作：1000<=year<=9999
 
    //         // 3.判断是闰年
    //         if (year % 4 === 0 && year % 100 !== 0 || year % 400 === 0) { //是闰年
    //             console.log('闰年');
    //         } else {
    //             console.log('平年');
    //         }
 
    //     } else {
    //         console.log('你输入的数字不是四位');
    //     }
 
    // } else { //不是数字
    //     console.log('输入有误，不是数字');
    // }
 
    // 1.3.多分支：多个选中
    /*
    结构：
    if(条件1){ 满足条件1执行的语句块}
    else if(条件2){ 满足条件2执行的语句块}
    else if(条件3){ 满足条件3执行的语句块}
    else if(条件4){ 满足条件4执行的语句块}
    else if(条件5){ 满足条件5执行的语句块}
    else if(条件6){ 满足条件6执行的语句块}
    ......
    else{ 其他条件执行的语句块 }
    */
 
    // 案例：输入一个分数，判断等级。
    var year = +prompt('请输入分数0-100'); //假定输入的是0-100,划分5个等级
    if (!isNaN(year)) {
        if (year === 100) {
            console.log('天才');
        } else if (year >= 90 && year < 100) {
            console.log('优秀');
        } else if (year >= 70 && year < 90) {
            console.log('良好');
        } else if (year >= 60 && year < 70) {
            console.log('及格');
        } else if (year >= 0 && year < 60) {
            console.log('不及格');
            // } else {
            //     console.log('输入有误');
            // }
        }
    } else {
        console.log("您输入的不是一个数字，请您重新输入！")
    }
 
    // 二.if语句的核心特点 - 重点
    // 1.if的条件可以是任意的表达式,但结果一定是布尔值，ES强制转换。
    // 2.else可以省略，else会产生短路操作。
    // 3.将最大的可能给if语句，优化if语句方式。
    // 意义是if语句执行了，else不执行，但是else语句执行if肯定执行。
    // var num = prompt('请输入一个数字');
    // if (!isNaN(num)) { //是数字
    //     console.log('是数字');
    // } else { //不是数字
    //     console.log('不是数字');
    // }

# 考试案例 1
<script>
     var numer = prompt('请输入本次考试的成绩：');
     if (numer == 100) {
      console.log ('满分');
     }
     else if (numer >= 90 && numer <= 99) {
      console.log ('优秀');
     }
     else if (numer >= 80 && numer<90) {
      console.log ('良好');
     }
     else if (numer >= 60 && numer <80) {
      console.log ('及格')
     }
     else if (numer >= 0 && numer <60) {
      console.log ('不及格')
     }
     else {
      console.log ('输入格式错误')
     }
</script>

# 考试案例 2
<script>
     var heiht = prompt('请输入身高cm')
         qian = prompt('请输入身价万')
         shuai =prompt('请输入颜值帅')
     if (heiht >= 180 && qian >= 1000 && shuai  >= 500) {
      console.log ('一定嫁给他')
     }
     else if (heiht >= 180 || qian >= 1000 || shuai  >= 500) {
      console.log ('勉强嫁给他')
     }
     else if (heiht < 180 && qian < 1000 && shuai  < 500) {
      console.log ('坚决不嫁')
     }
     else {
      console.log ('输入错误')
     }
</script>

#  一.对象：类下面的具体的事物 - 一切皆对象
        // 1.通过id名称获取标签，获取元素对象。
        // img标签：元素对象(element object),直接通过id名称获取标签
        // alert(pic); //[object HTMLImageElement]
        // src,alt,id：元素对象的属性
     
        // 2.通过元素对象获取属性以及设置属性。
        // console.log(pic.src); //获取图片的绝对路径
        // pic.src = 'img/3.jpg'; //设置
     
     
        // 3.元素对象添加方法(被动的方法)
        // 主动的方法：主动触发，直接使用。比如：alert/console.log/document.write
        // 被动的方法：事件(鼠标和键盘)。比如：onclick鼠标点击触发事件
        // var num = 1;
        // pic.onclick = function() { //function:函数，实现方法的结构体,点击pic，执行function下面{}里面的内容,每点击都会执行。
        //     num++;
        //     //仅存在5张图片，如果num>5没有图片了，利用判断让num>5的情况下重新变成1
        //     if (num > 5) {
        //         num = 1;
        //     }
        //     pic.src = 'img/' + num + '.jpg'; //字符串中出现变量，采用+进行拼接
        // };
# 图片切换案例 3
<style>
    .fahter {
      width: 400px;
      height: 400px;
      box-sizing: border-box;
      margin: 100px auto;
      position: relative;
    }
    #pic {
      width: 400px;
      height: 400px;
      object-fit: cover;
    }
    #l {
      width: 100px;
      height: 100px;
      position: absolute;
      left: -100px;
      top: 150px;
    }
    #r {
      width: 100px;
      height: 100px;
      position: absolute;
      right: -100px;
      top: 150px;
    }
  </style>
  <body>
    <div class="fahter">
      <img src="../img/1.png" alt="" id="pic" />
      <img src="../img/l.png" alt="" id="l">
      <img src="../img/r.png" alt="" id="r">
    </div>
  </body>
</html>
<script>
    var num = 1
    r.onclick = function () {
      num ++
      if (num > 4) {
        num = 1 
      }
      // pic.src = "../img/" + num + ".png"
      pic.src = `../img/${num}.png`
    }
    l.onclick = function () {
      num --
      if (num < 1) {
        num =4
      }
      pic.src = "../img/" + num + ".png"
    }
</script>

# 三。switch 语句
// 为什么学习switch分支语句，因为有了if分支语句。
    // 1.switch用来做多分支，注意和if的区别。
    // 2.switch语句的结构和解读
    /* 
        语法特点 - 重点
        switch括号里面的值恒等于case后面的某个值，执行case后面对应的语句块。
        每一个case都表示一个分支，case具有穿透力，需要给每一个情形后面添加break, break表示switch语句的结束
        default表示不满足任何一个case而执行的语句块，类似于if语句里面的else，default可以省略
         
 
        switch(值){
            case 值:  语句块;  break;
            case 值:  语句块;  break;
            case 值:  语句块;  break;
            case 值:  语句块;  break;
            case 值:  语句块;  break;
            case 值:  语句块;  break;
            case 值:  语句块;  break;
            ......
            default: 其他情况执行的语句块;
        }
    */
 
    // 案例一.简单了解switch语句的执行过程。
    // 输入数字0 - 6， 输出星期日 - 星期六
 
    // var num = +prompt('请输入数字0-6'); //字符串变成数字
    // switch (num) {
    //     case 0:
    //         console.log('星期日');
    //         break;
    //     case 1:
    //         console.log('星期一');
    //         break;
    //     case 2:
    //         console.log('星期二');
    //         break;
    //     case 3:
    //         console.log('星期三');
    //         break;
    //     case 4:
    //         console.log('星期四');
    //         break;
    //     case 5:
    //         console.log('星期五');
    //         break;
    //     case 6:
    //         console.log('星期六');
    //         break;
    //     default:
    //         console.log('输入有误');
    // }
 
    案例二， 输入一个月份输出这个月的天数 - 利用case穿透力完成。
    大月： 1, 3, 5, 7, 8, 10, 12 - 31 天
    小月： 4, 6, 9, 11 - 30 天
    平月： 2 - 闰年29天 平年28天
 
    点击按钮， 计算对应的天数
    所有的表单都是元素对象， 都对应有一个value属性表示表单里面的值。
    btn.onclick = function() { //点击按钮，执行后面的语句块
        var m = +month.value; //获取月份
        var y = +year.value; //获取年份
        switch (m) {
            // 利用case没有break情况下会穿透。
            case 1:
            case 3:
            case 5:
            case 7:
            case 8:
            case 10:
            case 12:
                result.value = '31天'; //赋值给结果的表单
                break;
            case 4:
            case 6:
            case 9:
            case 11:
                result.value = '30天'; //赋值给结果的表单
                break;
            case 2:
                //判断是否是闰年，再计算。
                if (y % 4 === 0 && y % 100 !== 0 || y % 400 === 0) { //是闰年
                    result.value = '29天'; //赋值给结果的表单
                } else {
                    result.value = '28天'; //赋值给结果的表单
                }
                break;
 
            default:
                result.value = '输入有误，请重新输入';
        }
    };
</script>
# 考试案例 4 判读是星期几
<script>
  var xiqi = prompt("请输入星期：");
  switch (+xiqi) {
    case 1:
    console.log("今天星期一");
      break;
    case 2:
    console.log("今天是星期二");
      break;
    case 3:
    console.log("今天是星期三");
      break;
    case 4:
    console.log("今天是星期四");
      break;
    case 5:
    console.log("今天是星期五");
      break;
    case 6:
    console.log("今天是星期六");
      break;
    case 7:
      console.log("今天是星期天");
      break;
    default:
    console.log('输入有误')
    break
  }
</script>

# 考试案例 5，判断是否是闰年
<script>
  var nian = prompt("请输入年份：");
  yue = prompt("请输入月份：");             1.先switch (+yue) 里设置3中case :，以break结束，再把年月的的设置嵌套在2月里
  switch (+yue) {
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
      console.log("这是大月");
      break;
    case 4:
    case 6:
    case 9:
    case 11:
      console.log("这是小月");
      break;
    case 2:
      if (+nian % 4 == 0 && +nian % 100 != 0 || +nian % 400 == 0) {    2.这个公式先放在-var nian = prompt("请输入年份：");里，再嵌套在2月里
        console.log("这个是29天");
      } 
      else {
        console.log("这个是28天");
      }
      break;
      default:
        console.log("输入错误");
      break;
  }

# 考试案例 6，用switch 语句，实现分数成绩
 var fenshu = prompt("请输入分数：");
  switch (true) {                               1.如果值为判断或区间的话，则switch（）内加true,
    case +fenshu == 100:                        2.变量的值为==
      console.log("满分");
      break;
    case +fenshu >= 90 && +fenshu < 100:        3.case 值可以为变量的区间
      console.log("优秀");
      break;
    case +fenshu >= 80 && +fenshu < 90:
      console.log("良好");
      break;
    case +fenshu >= 60 && +fenshu < 80:
      console.log("及格");
      break;
    case +fenshu < 60:
      console.log("不及格");
      break;
    default:
      console.log("输入有误");
      break;
  }

# 四 一.switch和if语句的区别 - 非常重要
    // 一般情况下，这两个语句是可以相互替换的；
    // 1.switch语句通常处理case为比较确定的值的情况，而if...else...语句更加灵活，常用于范围判断（大于、等于、小于某个范围）；
 
    // 2.switch语句进行条件判断时，找到对应的条件直接执行，效率更高。而if...else...语句，有几种条件，就得进行几次判断。
 
    // 结论：
    // 当分支比较少的时候，if...else...语句的执行效率比switch语句高；
    // 当分支比较多时时候，switch的执行效率高，而且结构清晰。
 
    // var num = 5;
    // switch (num) {
    //     case 1:
    //         console.log(1);
    //         break;
    //     case 2:
    //         console.log(2);
    //         break;
    //     case 3:
    //         console.log(3);
    //         break;
    //     case 4:
    //         console.log(4);
    //         break;
    //     case 5: //一步到位，找到对应的条件直接执行，效率更高
    //         console.log(5);
    //         break;
    // }
 
 
    // if (num === 1) {
    //     console.log(1);
    // } else if (num === 2) {
    //     console.log(2);
    // } else if (num === 3) {
    //     console.log(3);
    // } else if (num === 4) {
    //     console.log(4);
    // } else if (num === 5) { //执行到第五步才会执行。
    //     console.log(5);
    // }
 
 
    // 通过switch改写if语句
    // 案例：输入一个分数，判断等级。
    // var score = +prompt('请输入分数0-100'); //假定输入的是0-100,划分5个等级
    // if (score === 100) {
    //     console.log('天才');
    // } else if (score >= 90 && score < 100) {
    //     console.log('优秀');
    // } else if (score >= 70 && score < 90) {
    //     console.log('良好');
    // } else if (score >= 60 && score < 70) {
    //     console.log('及格');
    // } else if (score >= 0 && score < 60) {
    //     console.log('不及格');
    // } else {
    //     console.log('输入有误');
    // }
 
 
    var score = +prompt('请输入分数0-100'); //假定输入的是0-100,划分5个等级
    switch (true) { //switch改写if语句，这里的值基本上都是布尔值。
        case score === 100:
            console.log('天才');
            break;
 
        case score >= 90 && score < 100:
            console.log('优秀');
            break;
 
        case score >= 70 && score < 90:
            console.log('良好');
            break;
 
        case score >= 60 && score < 70:
            console.log('及格');
            break;
 
        case score >= 0 && score < 60:
            console.log('不及格');
            break;
 
        default:
            console.log('输入有误');
    }
