# 一.TypeScript的介绍

1. TypeScript 是加强版的 JavaScript

2. TypeScript 是用来规范 js 的

3. TypeScript 实在大型项目开发的时候使用，是的代码桁架规范，协助更加友好，维护桁架便利

4. TypeScript 报错，在编写的时候报错


# 二.TypeScript的安装

1. npm i typescript -g

2. 编译 ts
命令行输入：tsc ./src/index.ts --outFile ./dist/index.js

3. 此时会多出一个 dist文件夹的 index.js文件

4. 实时监听：
<!-- 每一次在 src 文件夹的 index.js 写完之后，都要在命令行中输入 tsc ./src/index.ts --outFile ./dist/index.js-->
<!-- 为了使 dist文件夹的 index.js文件 与之达到同步-->
在命令行中输入：tsc --init //初始化 ts配置文件

5. 此时，在 src文件中，会多出一个 tsconfig.json 的文件

6. 在 tsconfig.json 的文件中，将 "module": "commonjs", 下面的 // "rootDir": "./",  改为： "rootDir": "./src",   

7. 在 tsconfig.json 的文件中，将 "module": "commonjs", 下面的 // "outDir": "./",  改为：// "outDir": "./dist",  

8. 在命令行中输入：tsc --watch //实时监听 ts

9. dist文件夹的 index.js文件的内容为：
"use strict";
let str = "hello";



# 三.ts 的类型判断

<!-- 定义字符串 -->
let str1: string = "hello";
str1 = "8888"

let str2: string;
str2 = "hello"

<!-- 定义数字 -->
let num1: number = 10;
num1 = 8888

let num2: number;
num2 = 8888

<!-- 定义布尔值 -->
let done:  boolean = true;
done = false

<!-- 定义 undefined，定义好了，就不能更改了 -->
let udf:  undefined = undefined;

<!-- 定义 null，定义好了，就不能更改了 -->
let nl:  null = null;


# 四.ts 联合类型

<!-- 多种类型 -->
let arr: number | string | boolean = 10;
arr = "hello"
arr = true

<!-- 多种类型 -->
let a: number | null ;
a = 10

<!-- 多种类型 -->
let b: string | null = localStorage.getItem("token");
if(b){
 <!-- 因为 token 一定是字符串，有可能 token 刚开始不存在，为 null，那 token 就不可能有split(",")的方法，所以先定义 b 存在-->
  b.split(",")
}


# 五.ts 任何类型 any
<!-- any:一般不准随便使用 -->
let abc: any = 4
abc = [1,2,3]

# 六 ts 数组的类型
<!-- 数字的数组 -->
let arr1: number[] = [1,2,3,]

<!-- 字符串的数组 -->
let arr2: string[] = ["1","2","3","4"]

<!-- 由数字、字符串和布尔值，组成的数组 -->
let arr3: (number | string | boolean)[] = [1,"2",true]

<!-- 由数字和数字类型的数组，组成的数组 -->
let arr4: (number | number[])[] = [1,2,[3,4,5]]

<!-- 由对象组成的数组 -->
let arr5: object[] = [{a:1},{b:2},{c:3}]  //错误

<!-- any任意 类型的 -->
let arr7: any = [1,2,[3,4,5]]

# 七. ts 数组的元组类型
<!-- 元组类型 ，可以规定：数组的长度，还可以规定数组每一项的数组类型-->
let arr8: [number,string] = [1,"zhangsan"]


# 八. ts 对象类型

1. 对象类型
<!-- 对象类型的定义，需要使用 interface 的接口 -->
interface ObjType {
    name:string;
    age:number;
    sex?:number;
    <!-- ?,表示可选项 -->
    [propname:string]:any
    <!-- 索引签名：可以传入任何类型 -->
}

let obj1: ObjType = {
    name:"zhangsan",
    age:20
}

obj1.sex = 1

2. 对象类型的数组
<!-- 对象类型的定义，需要使用 interface 的接口 -->
interface ItemType {
    id:number,
    name:string
}

let arr : ItemType[] = [
    {
        id:1,
        name:"zhangsan"
    },
    {
        id:2,
        name:"lisi"
    }
]

3. 对象嵌套数组
interface ItemType {
    id:number;
    name:string;
    children?:ItemType[]
    <!-- （有的有children，有的没有children）： children为：ItemType[]--数组内有对象-->
}

let arr2: ItemType = {
    id:1,
    name:"zhansan",
    children:[
        {
            id:2,
            name:"lisi",
            children:[
                {
                    id:4,
                    name:"wangwu"
                }
            ]
        },
        {
            id:3,
            name:"laoliu"
        }
    ]
}


# 九. ts 函数类型 

1. 数字的函数
function add(x:number,y:number):number{
    <!-- x:数字，y:数字    返回的也是数字 -->
    return x + y  //7
}
add(3,4)

2. 数字加字符串的函数
function add(x:number,y:string):string{
   <!-- x:数字，y:字符串    返回的是字符串 -->
    return x + y  // 3"zhangsan"
}
add(3,"zhangsan")

3. 定义变量的函数
const add2 = (x:number,y:number):number =>{
<!-- <!-- 定义add2 等于 x:数字，y:字符串 ，返回的是数字-> -->
    return x + y
}
add2(3,4)

4. 函数的可选参数
<!-- 必选参数必须放在可选参数的前面 -->
function fn1(a:number,b?:number):number{
                    <!-- b?:可选参数 -->
    if(b){
      return a + b
    }else{
      return a
    }
}
fn1(3)









































