# 一：javascript :

1.外部：单独的文件 <script src="外部"></script> 2.内部：html 文件的内部 <script>内部</script>

# 二：变量：var

     var    num   = 10；  定义一个变量unm
     变量  随便起  变量值

     var    n1 = 1,
     var    n2 = 2,
     var    n3 = 3；   定义多个变量

    1.概念：所谓变量，就是特定时间用于保存特定值的一个名字而已，并且初始化后可以再次改变的量。

    2.声明定义：
        使用var是关键字，后面跟一个变量名（变量名是标识符,标识符就是自定义的名称）,声明多个变量的时候，可以在一行或者多行操作，只要把每个变量用逗号分隔开即可，但最好分行写，可读性佳。
        关键字：作者约定的具有特殊意义的单词。

    3.变量的特点：
        变量会写入内存，script里面任意使用变量

        变量访问输出(赋值)
        var    num   = 10；

        变量前置访问输出undefined(未初始化，未赋值) ---值依然存在，没有显示
        alert   var    num   = 10；

# 三：变量：var 的使用和写法

1.重复使用的值存为变量，方便修改，变量可以将程序代码变的更灵活

<script>
  var num1 = 111,mun2 = 222,unm3 = 333;
  alert(num1+"我们是优秀的")
  alert(num1+"我们是很棒的")
  alert(num1+"我们是最好的")
</script>

# 四：变量的数据类型：

    // 一.数据类型
    // ES语法中，每一个值对应一种类型，通过类型确定值的结构

    // 1.数字类型，js的数字类型不区分整数和小数,都称之为number。
    // var a = 1;
    // var b = 3.14;

    // 2.字符串类型，程序中的一些符号，中英文，需要添加引号(单双引号都可以),都称之为string
    // var str = 'hello';
    // var str1 = '我是前端开发人员';
    // var str2 = "world";
    // var str3 = "3241$%$(*&(";

    // 3.布尔值类型，布尔类型只有两个值，true和false分别表示真和假,都称之为boolean
    // var b1 = true;
    // var b2 = false;
    // console.log(true); //true

    // 4.undefined类型，表示变量未赋值，未初始化，属性不存在等。
    // var a;
    // console.log(a); //undefined
    // console.log(window.hehe); //undefined

    // 5.null类型，空对象类型。
    // var a = null; //表示a是空对象。


    // 6.object类型，对象类型，复杂类型，复合类型。


    // 二.数据类型的分类
    // 1.基本类型：number/string/boolean/null/undefined
    // 2.对象类型(引用类型)：object


    // 三.如何检测数据类型
    // tpyeof 关键字直接检测值的类型，但是typoef检测输出的值都是字符串类型 。
    // console.log(typeof 123); //number
    // console.log(typeof typeof 123); //string

    // var a = 1;
    // var b = 'hello';
    // var c = true;
    // var d = null;
    // var e = undefined;
    // var f = {};

    // console.log(typeof a); //number
    // console.log(typeof b); //string
    // console.log(typeof c); //boolean
    // console.log(typeof d); //object - 注意
    // console.log(typeof e); //undefined
    // console.log(typeof f); //object


    // 四.特殊的数据类型：undefined和null
    // 企业级语言null和undefined表示的意思是一样的。
    // 所以js里面null和undefined的值是相等的，但是类型不相等。

# 五，对象

    // 一.window代码演示
    // window.alert(1);
    // window.alert(2);
    // window.alert(3);
    // window.prompt('请输入用户名：'); 输入框
    // confirm('你确定要删除吗?');  删除框

    // 二.document对象的代码演示
    // window.document.write('你好，欢迎学习js');
    // window.document.write('<hr>');
    // window.document.write('welcome');
    // window.document.write('<hr>');
    // window.document.write('<h1>我是大标题标签</h1>');

    // 三.console对象的代码演示  控制台
    // console.log(1 + 1);
    // console.log(1, 2, 3, 4, 5, 6);

# 六：赋值、数学、关系运算符的讲解

// 一.赋值运算符
// 1.=号
// var a = 1;//意义：将右边的 1 赋值给左边的 a
// var b = 2;
// b = b + 1; //将上面的 b 先+1 再赋值给 b
// console.log(b); //3

// 2.复合的赋值运算符
// 复合赋值操作 +=、-=、\*=、/=、%= 带操作的复合赋值运算,（更快捷，更优）
// var b = 2;
// b += 1 //b = b + 1;
// console.log(b);

// var a = 10;
// a -= 100;
// console.log(a); //-90

// 二.数学运算符
// 1.+号:三种用途
// 1.1.加法运算
// console.log(1 + 2); //3
// console.log(0.1 + 0.2); //0.30000000000000004 计算机产生的误差，因为二进制小数产生的误差。
// console.log(0.1 + 0.5); //0.6
// console.log(0.2 + 0.4); //0.6000000000000001

// 解决：将数字扩大成整数，进行运算符，结果对应缩小
// console.log((0.1 _ 10 + 0.2 _ 10) / 10); //0.3

// 1.2.拼接符号，只有符号两边任意一边出现字符串，变成拼接符号,结果都变成字符串。
// var name = '张三';
// console.log('我的名字是' + name);

// var a = 11;
// var b = '89';
// console.log(a + b); //1189

// var a = 10;
// var b = 20;
// var c = 30;
// console.log(a + b + c + '');
// console.log(342857348);

// 1.3.当做正号使用，将任意类型的值转换成数字,如果无法转换，输出 NaN（not a number:不是一个数字)
// var n1 = '123';
// var n2 = '100';
// console.log(typeof n1); //string
// console.log(typeof + n1); //number

// console.log(n1 + n2); //123100
// console.log(+n1 + +n2); //223

// var n3 = 'hello';
// console.log(+n3); //NaN,作者约定的关键字

// 2.%(取余或者求模)：求两个数相除的余数。
// console.log(9 % 2); //1
// console.log(2 % 9); //2

// 应用场景：
// 当两个数的余数为 0，确定这两个数能够整除。
// 如果前面的数小于后面的数，结果就是前面的数。
// x 是任意的正整数，结果一定是 0,1,2,3,4 console.log(x%5)

// 3.其他符号：- _ /
// 其他符号都具有转换功能，将字符串格式的数字转换成真正的数字，如果不能运算返回 NaN
// var a = '3';
// var b = '5';
// console.log(a + b); //字符串 35
// console.log(a - b); //-2
// console.log(a _ b); //15
// console.log(a / b); //0.6
// console.log(a % b); //3

// 三.关系运算符:结果是布尔值(true/false)
// <、>、<=、>=、==( 相等 )、===（全等）、!=(不相等) !==（不全等）

// var a = 1;
// var b = 2;
// var c = 1;
// console.log(a > b); //false
// console.log(a >= c); //true a 大于或等于 c 都可以

// 1.==相等，比较的是值，和类型没有关系，而且尽最大的努力将值转换成数字进行比较。
// 数字比较
// console.log('5' == 5); //true
// console.log(true == 1); //true
// console.log(+true); //1
// console.log(null == undefined); //true 没有任何解释，就是作者的约定。
// console.log(+null); //0
// console.log(+undefined); //NaN
// 字符串的比较
// 逐个字母进行比较，将字母转换成 unicode 编码进行比较。
// A-Z 65-90
// a-z 97-122
// 0-9 48-57

// console.log('zhangsan' > 'lisi'); //true
// console.log('banana' > 'apple'); //true

// 2.===:恒等，全等，值和类型都要相等,不会进行转换。
// console.log('5' === 5); //false
// console.log('5' === '5'); //true

// 3.如果是数字和字符串比较，转换成数字
// console.log('abc' > 10); //NaN > 10 false
// console.log(true >= 1); //1>=1 true

# 七：变量不同类型之间的转换

// 一.变量不同类型之间的转换
// 1.显式转换：利用系统提供的函数(具有特定功能的代码块组成)强制转换或者手动转换
// 强制转换函数：Number() 、String() 、Boolean()
// 1.1.Number()：将括号里面的值强制转换成数字，如果无法转换输出 NaN
// console.log(Number('')); //0
// console.log(Number(' ')); //0
// console.log(Number('hello')); //NaN
// console.log(Number(null)); //0
// console.log(Number(undefined)); //NaN
// console.log(Number('5')); //5
// console.log(Number('5abc')); //NaN

    // 1.2.String():将括号里面的值强制转换成字符串，相当于给当前的关键字添加了引号
    // console.log(true);
    // console.log(String(true));
    // console.log(String(null));
    // console.log(String(undefined));

    // 1.3.Boolean():将括号里面的值强制转换成布尔值(true/false)
    // 规律：数字非0即真，字符串非空即真，null，undefined,NaN都是false  - 重点
    // console.log(Boolean(0)); //false  数字非0即真
    // console.log(Boolean('')); //false  字符串非空即真
    // console.log(Boolean(' ')); //true
    // console.log(Boolean(null)); //false
    // console.log(Boolean(undefined)); //false
    // console.log(Boolean(NaN)); //false


    // 总结：
    // 上面的三个方法来自于作者的一厢情愿，开发中意义不大，因为都可以利用符号简单取代
    // Number() -> +
    // String() -> ''
    // Boolean() -> !!


    // 2.window下面的方法
    // 类->对象->(属性和方法)
    // window.parseInt():将括号里面的字符串转换成数字(整数)，从第一个数字字符串开始转换，碰到非数字字符串结束 - 重点
    // console.log(parseInt('123abc')); //123
    // console.log(parseInt('123px')); //123
    // console.log(parseInt('200.99px')); //200
    // console.log(parseInt('0.99px')); //0
    // 上面的方法可以跟进制有关，暂时忽略。


    // window.parseFloat()：将括号里面的字符串转换成数字(包括小数)，从第一个数字字符串开始转换，碰到非数字字符串结束
    // console.log(parseFloat('3.14px')); //3.14


    // 3.隐式转换：系统自动根据当前的符号进行转换(+,-,*,/,%,==,++,--)


    // 案例：
    // console.log(parseInt('2*2.3')); //2

    // 1.为抵抗洪水，战士连续作战89小时，编程计算共多少天零多少小时？
    // 考察的基础：
    // 拼接
    // 变量
    // 输入：prompt

    // var day = parseInt(89 / 24);
    // var hour = 89 % 24;
    // console.log('为抵抗洪水，战士连续作战89小时，编程计算共' + day + '天零' + hour + '小时');

    // var allHour = prompt('请输入战士连续作战小时数：'); //prompt输入的值都是字符串
    // var day = parseInt(allHour / 24);
    // var hour = allHour % 24;
    // console.log('为抵抗洪水，战士连续作战' + allHour + '小时，编程计算共' + day + '天零' + hour + '小时');


    // 2.输入一个五位数，分别输出个十百千万位；
    // var num = 12345;
    // console.log(num % 10);
    // console.log(parseInt(num % 100 / 10));
    // console.log(parseInt(num % 1000 / 100));
    // console.log(parseInt(num % 10000 / 1000));
    // console.log(parseInt(num / 10000)); //万.

# 八.逻辑运算符：

     假的布尔值为：（"）（0）（false）（null）（undefined）
    // 逻辑运算符
       1.&& - and - 和
    // 逻辑与(&&)操作可以应用于任何类型的操作数，而不仅仅是布尔值。在有一个操作数不是布尔值的情况下，逻辑与操作就不一定返回布尔值。逻辑与操作属于短路操作，即如果第一个操作数能够决定结果，那么就不会再对第二个操作数求值。

    // 操作数为假的情况：0 '' null undefined NaN false 其他的都是为真。

    // console.log(3 && 4); //4
    // console.log(3 && false); //false
    // console.log(0 && false); //0
    // console.log(false && 这里我在乱写); //false 短路操作(跳过程序不执行)
    // 解析二个操作数的过程：
    // 对第一个操作数进行操作(转布尔值操作)，如果第一个操作数为真,结果就是第二个操作数的值。
    // 如果第一个操作数为假，结果是第一个操作数的值，形成短路操作。
    // 总结：逻辑与找的假的立刻结束，形成短路。

    // console.log(1 && 2 && 3); //3
    // console.log(1 && 0 && 3); //0
    // console.log(1 && false && false); //false
    // console.log(0 && 1 && 2 && 3); //0


       2.|| - or - 或
    // 逻辑或(||)和逻辑与操作相似，如果有一个操作数不是布尔值，逻辑或也不一定返回布尔值，逻辑或操作符也是短路操作符。也就是说，如果第一个操作数的求值结果为true ，就不会对第二个操作数求值了。

    // console.log(1 || 2 || fkdlasjflkdsajfkl); //1 形成短路
    // console.log(0 || 0 || fkdlasjflkdsajfkl); //报错
    // console.log(0 || '' || false); //false

       3.! - not - 非
    // 逻辑非操作符由一个叹号（！）表示，可以应用于ES中的任何值。无论这个值是什么数据类型，这个操作符都会返回一个布尔值。逻辑非操作符首先会将它的操作数转换为一个布尔值，然后再对其求反。
    // console.log(!3); //false
    // console.log(!!3); //true
    // console.log(!!!!!3); //false


    // 整理规则
    // && 和 || 两个符号操作数都要转换成布尔值进行运算，但结果不一定是布尔值。
    // 逻辑与找的假的立刻结束，形成短路.
    // 逻辑或找到真的立刻结束，形成短路.
    // 逻辑非的结果一定是布尔值，然后取反.

# 九： 一.一元运算符：++ --

    // 只能操作一个值的操作符叫做一元操作符，是 ECMAScript 中最简单的操作符。
    // 前置型应该位于要操作的变量之前，先将操作数+1或者减1，再参与运算。
    // 后置型则应该位于要操作的变量之后，先参与运算后自身再+1或者减1。

    // 1.++运算符：不管++在操作数的前面还是后面都是自身+1
    // var a = 1;
    // a++; // 相当于a = a + 1  a += 1;
    // console.log(a); //2
    // 1.1.如果++在操作数的前面（前置型）：先将操作数+1，再参与运算。
    // var a = 1;
    // var b = ++a; //先a自身+1，赋值给b
    // console.log(a); //2
    // console.log(b); //2

    // 1.2.如果++在操作数的后面（后置型）：先参与运算，再自身+1。
    // var a = 1;
    // var b = a++; //先赋值给b，a自身+1
    // console.log(a); //2
    // console.log(b); //1

    // var a = 1;
    // var b = a++ + ++a + a++ + a;
    // console.log(a); //4
    // console.log(b); //11


    // var a = 1;
    // var b = ++a + a++;
    // var c = ++b + b++ + ++a + a++;
    // console.log(a); //5
    // console.log(b); //6
    // console.log(c); //18

    // 注意
    // var a = 1;
    // console.log(a++); //1 这里输出的是等式a++
    // console.log(a); //2 这里输出a的值

    // 和上面同步的
    // var a = 1;
    // var b = a++;
    // console.log(b); //1
    // console.log(a); //2

    // 例如：
    var k = 0;
    //k的结果：  1      2    2   3
    //等式的结果：0      2    2   2
    console.log(k++ + ++k + k + k++); //6
    console.log(k); //3

# 十： NaN 和 isNaN 介绍

    // 1.当数学计算无法得到数字结果，该变量的值为NaN(not a number)
    // 注意的地方：
    // console.log(NaN == NaN); //false
    // console.log(typeof NaN); //number 虽然表示的不是一个数字，依然属于数字类型。
    // console.log(typeof typeof NaN); //string

    // 2.isNaN(num)函数，该函数判断num变量的值是否是NaN（不是一个数字）,结果是布尔值,如果num不是一个数字输出true
    // console.log(isNaN('abc')); //true  不是数字
    // console.log(isNaN('100abc')); //true 不是数字
    // console.log(isNaN(100)); //false
    // console.log(isNaN('100')); //false  这里也是数字，可以将字符串格式的数字换成真正的数字。

# 十一:一.核心的内容 - 重点

    1.变量
        - 变量的特点(变量提升，写入内存，声明多个,初始化之后还可以改变，松散类型)
        - 变量的命名 - 小驼峰命名
        - 变量的数据类型 - 6种(基本类型和引用类型)
        - 变量类型的检测 - typeof(返回值都是字符串类型)

    2.运算符
        - 赋值运算符 +=  =
        - 数学运算符 + %
        - 关系运算符 > < >= <= == === != !==
        - 逻辑运算符 && || !
        - 一元运算符 ++ --

    3.隐式转换
        - + - * / % ++ -- == !

    4.类，对象，属性，方法
        - 概念
        - 方法
            - alert
            - prompt
            - confirm
            - parseInt
            - parseFloat
            - console.log
            - document.write

    二.学习网站
    1.碰到问题，多沟通，可以百度搜索

    2.学习网站
    CSDN：https://www.csdn.net/   学习网站
    力扣： https://leetcode-cn.com/problemset/all/  算法提升网站
    牛客网：https://www.nowcoder.com/  算法提升网站

    3.算法
    前端其实对算法的需要时中等的，算法的提高是需要时间的，如果每天刷一两道算法题，可以提升算法，记得持之以恒。
