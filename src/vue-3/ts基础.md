# 一.ts 的可选参数

1. 函数的可选参数
<!-- 必选参数必须放在可选参数的前面 -->
function fn1(a:number,b?:number):number{
                    <!-- b?:可选参数 -->
    if(b){
      return a + b
    }else{
      return a
    }
}
fn1(3)//b的参数可不填

2. 没有返回值，专门给函数用的
function fn2() :void {
    <!--void  没有返回值，专门给函数用的-->
    console.log(123); 
}
fn2()

3. never 表示：从不，用于函数，解决函数死循环或者报错
function fn3():never{
    <!--never 表示：从不，用于函数，解决报错-->
  throw new Error("xxx")
}
fn3()

4. never 表示：从不，用于函数，解决函数死循环或者报错
function fn4():never{
    <!--never 表示：从不，用于函数，解决死循环-->
  while (true){}
}
fn4()

5. x,y要求传过来的类型一致
function fn5<T>(x:T,y:T){
    <!-- T代表 number 的类型 -->
  return 123
}
fn5<number>(3,4)

6. vue3 中的 定义类型
const count = ref<number>(5)



# 二.类:创建实例对象

1. 定义一个类
class Animal {
    names：string = "dog";
    sayName()：string{
        return this.names
    }
}

2. 继承 Animal的构造函数

class cat Animal {}

const cat = new cat()

console.log(cat.names)//"dog"



