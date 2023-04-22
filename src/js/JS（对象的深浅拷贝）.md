# 一.对象的深浅拷贝：
1. 浅拷贝: 拷贝对象的地址
2. 深拷贝：拷贝对象的数据
3. 栈内存存放: 基本类型的值和引用类型的地址
4. 堆内存存放: 引用类型的值

# 二.引用类型的深浅拷贝:
1. 浅拷贝：只能拷贝一层
2. 深拷贝：不限层数

# 三.对象的深浅拷贝

   浅拷贝：
1. 直接=的方式，会拷贝原来的值
<script>
  let obj1 = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 20
 }
 obj2 = obj1
 obj2.name = '里古拉斯'
 console.log(obj1)//{name: "zhangsan", age: "lisi", sex: 20}
 console.log(obj2)//{name: "zhangsan", age: "lisi", sex: 20}

2. 利用直接=的方式+Object.assign({},obj1)方式拷贝，不会改变原来的值
<script>
  let obj1 = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 20
 }
 let obj2 = Object.assign({},obj1) //合并对象
 obj2.name = '里古拉斯'
 console.log(obj1)
 console.log(obj2)
 </script>

3. 利用for.in遍历逐个拷贝:
            ----防止原型链新加的属性也会拿到
<script>
 let obj1 = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 20
 }
 let obj2 = {}
 for (let key in obj1) {
    if (Object.hasOwnProperty(key)){ //判断当前的key是不是实例对象自身的，干掉原型链新加的属性
      obj2[key] = obj1[key] //遍历obj1的值，obj2的值 = obj1的值
    }
 }
 obj2.name = '里古拉斯' //改变boj2的值，不会影响obj1的值
 console.log(obj1) //{name: "zhangsan", age: "lisi", sex: 20}
 console.log(obj2) //{name: "里古拉斯", age: "lisi", sex: 20}
</script>



  深拷贝：
利用直接=的方式+JSON方式拷贝，不会改变obj1的值
<script>
  let obj1 = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 20
 }
 let obj2 = JSON.parse(JSON.stringify(obj1))
 obj2.name = '里古拉斯'
 console.log(obj1)//{name: "zhangsan", age: "lisi", sex: 20}
 console.log(obj2)//{name: "里古拉斯", age: "lisi", sex: 20}



4. 利用for.in遍历逐个拷贝:
            ----防止原型链新加的属性也会拿到
<script>
 let obj1 = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 20
 }
 let obj2 = {}
 for (let key in obj1) {
    if (Object.hasOwnProperty(key)){ //判断当前的key是不是实例对象自身的，干掉原型链新加的属性
      obj2[key] = obj1[key] //遍历obj1的值，obj2的值 = obj1的值
    }
 }
 obj2.name = '里古拉斯' //改变boj2的值，不会影响obj1的值
 console.log(obj1) //{name: "zhangsan", age: "lisi", sex: 20}
 console.log(obj2) //{name: "里古拉斯", age: "lisi", sex: 20}
</script>

# 三.数组的深浅拷贝

   浅拷贝
<script>
 let arr1 = [{name: 'phoe',age: 1},{name: 'dfdfd', age: 2},]
 let arr2 = arr1

   深拷贝
 let arr1 = [{name: 'phoe',age: 1},{name: 'dfdfd', age: 2},]
 console.log(arr1)
 let arr2 = JSON.parse(JSON.stringify(arr1))
 console.log(arr2)
</script>


# 四.javascript值传递和址传递
1. 值传递，基本类型遵循的

2. 引用传递，引用类型（Object）遵循的，也可以叫做地址传递
   --引用类型将地址存放在栈内存中，值存放在堆内存中

# 五.基本类型和引用类型的赋值方式：
1. 基本类型的如果想彼此赋值，采用直接赋值的方式完成，如：
     let arr = 10
     let brr = arr

2. 引用类型如果想彼此赋值，不能直接赋值，必须采用拷贝的方式，将值逐个传递



# 五.浅拷贝的方式：
1. 利用for.in遍历逐个拷贝:
            ----但是会包括原型链新加的属性都会拿到
<script>
 let obj1 = {
  name : 'zhangsan',
  age : 'lisi',
  sex : 20
 }
 let obj2 = {}
 for (let key in obj1) {
    if (Object.hasOwnProperty(key)){ //判断当前的key是不是实例对象自身的，干掉原型链新加的属性
      obj2[key] = obj1[key] //遍历obj1的值，obj2的值 = obj1的值
    }
 }
 obj2.name = '里古拉斯' //改变boj2的值，不会影响obj1的值
 console.log(obj1) //{name: "zhangsan", age: "lisi", sex: 20}
 console.log(obj2) //{name: "里古拉斯", age: "lisi", sex: 20}
</script>

2. 封装函数实现浅拷贝：
