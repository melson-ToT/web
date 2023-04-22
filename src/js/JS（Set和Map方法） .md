# 二.Symbol--表示独一无二的值，属于基本类型
     ----对象的属性Symbol是一个原始值，不是对象
     
# 三.Set(array)和Map(object)结构
     ----Set（）针对数组
     ----Map（）针对对象
# (一).Set 本身是一个构造函数，用来生成Set数据结构，数组作为参数，并且会把数组内的同样的参数删除，返回一个独立的结构

# 案例1：
 <script>
let arr = ['zhangsan','lisi',100,200,'zhangsan','lisi',100,200]
console.log([...new Set(arr)])
</script>

1. size :长度属性
let s1 = new Set(['zhangsan','lisi',100,200])
console.log(s1.size); // 4

2. add():添加一个数据，返回Set本身
let s1 = new Set(['zhangsan','lisi',100,200])
let s2= [...s1.add('wangwu')]
console.log(s2);  //(5) ["zhangsan", "lisi", 100, 200, "wangwu"]

3. delete(value):删除指定的数据，返回布尔值
let s1 = new Set(['zhangsan','lisi',100,200])
s1.delete('zhangsan')  ----删除s1的'zhangsan'
let s2 = [...s1]
console.log(s2);//['lisi',100,200]

4. has(value):删除指定的数据，返回布尔值
let s1 = new Set(['zhangsan','lisi',100,200])
console.log(s1.has('zhangsan'));//true

5. has(value):删除指定的数据，返回布尔值
let s1 = new Set(['zhangsan','lisi',100,200])
console.log(s1.clear());//undefined

6. forEach():遍历数据

# Map结构：
# 案例1：

1. size :长度属性
let s1 = new Map(['zhangsan','lisi',100,200])
console.log(s1.size); // 4

2. add():添加一个数据，返回Map本身
let s1 = new Map(['zhangsan','lisi',100,200])
let s2= [...s1.add('wangwu')]
console.log(s2);  //(5) ["zhangsan", "lisi", 100, 200, "wangwu"]

3. delete(value):删除指定的数据，返回布尔值
let s1 = new Map(['zhangsan','lisi',100,200])
s1.delete('zhangsan')  ----删除s1的'zhangsan'
let s2 = [...s1]
console.log(s2);//['lisi',100,200]

4. has(value):删除指定的数据，返回布尔值
let s1 = new Map(['zhangsan','lisi',100,200])
console.log(s1.has('zhangsan'));//true

5. has(value):删除指定的数据，返回布尔值
let s1 = new Map(['zhangsan','lisi',100,200])
console.log(s1.clear());//undefined

