# 一：Object.defineProperty()方法
  Object.defineProperty()方法，会在对象上添加一个新属性，或者修改对象的现有属性，并返回给对象

# 二.Object.defineProperty()方法的使用

1. 添加一个新属性
<script>
const obj={
  name : 'zhangsan'
}
Object.defineProperty(obj,'age',{//第一个值为：对象，第二个值为：添加的属性
    value:'20岁'                 //{}内的value为：第二个属性的属性名称，'20岁'为属性值
    })
console.log(obj)//{name: "zhangsan", age: "20岁"}
 </script>

2. 修改属性
<script>
const obj={
  name : 'zhangsan'
}
Object.defineProperty(obj,'age',{
  value:'20岁',
  writable:true         //如果添加的属性要进行修改的话，配置项必须加一个writable为true
})                      //本身writable为false
console.log(obj)//{name: "zhangsan", age: "20岁"}
obj.age = '30岁'
console.log(obj)//{name: "zhangsan", age: "30岁"}
 </script>

3. 删除对象内的属性
<script>
const obj={
  name : 'zhangsan'
}
Object.defineProperty(obj,'age',{//第一个值为：对象，第二个值为：添加的属性
    value:'20岁'                 //{}内的value为：第二个属性的属性名称，'20岁'为属性值
    configurable:true            //configurable:true添加删除功能
    })
delete.obj.age                   //删除age
console.log(obj)//{name: "zhangsan"}
 </script>

4. 遍历对象内的属性
<script>
const obj={
  name : 'zhangsan'
}
Object.defineProperty(obj,'age',{//第一个值为：对象，第二个值为：添加的属性
    value:'20岁'                 //{}内的value为：第二个属性的属性名称，'20岁'为属性值
    enumerable:true              //enumerable:true 添加遍历对象功能
    })
for(let key in obj){
  obj(key)                       //遍历对象功能
}             
console.log(obj)//{name: "zhangsan", age: "30岁"}
 </script>

# 三.存取器描述：----get属性和set属性，会起到监听效果
1. get属性：是一个函数，叫做getter获取器
            获取属性值的时候会自动调用,get方法返回的值就是获取的属性值

2. set属性：是一个函数，叫做setter设置器
            设置属性值的时候会自动调用，设置的值自动传递给set函数的参数

3. 当使用了getter获取器或setter设置器，不允许使用writable和value这两个属性（会报错）

<script>
const obj={
  name : 'zhangsan'
}
Object.defineProperty(obj,'age',{
  get(){
    console.log('get方法里面的值')
    return value //4.获取set的值
  },
  set(v){     //自带value属性
    console.log('set方法里面的值');
    value = v //3.设置100 = v
  }
})
obj.age = 100  //1.设置age的value为100
console.log(obj.age)
 </script>

# 四.数据劫持（绑定）：  ----数据代理
1. Model-View-ViewModel(简称MVVM)
2. --Model:      用户的界面，前端主要由HTML和CSS来构建
3. --View:       试图模型层
4. --ViewModel:  数据模型

# 五.数据驱动试图
1. 数据值指的是渲染的普通数据
2. 试图（HTML,渲染出来的结构）



# 六.数据劫持：VUE2.0   Object.defineProperty()
              其实就是数据代理，将原数据复制一份，利用复制的数据进行渲染，不影响原来的数据

              指的是：在访问或修改对象的某个属性时，通过一段代码拦截这个行为，进行额外的操作或者修改返回结果
<body> 
  <input type="text">
  <input type="text">
  <input type="text">
  <div class="box"></div>
</body>
</html>
</html>
<script>
const input= document.querySelectorAll('input')
const box = document.querySelector('.box')
const obj1 = {
  name : '张三',
  age : '男',
  sex : 24
}
const obj2 = {}
Object.defineProperty(obj2,'name',{
  get(){
    return obj1.name
  },
  set(v){
    obj1.name = v
    box.innerHTML = obj2.name
  }
})
input[0].oninput = function(){
  obj2.name=this.value
}
Object.defineProperty(obj2,'age',{
  get(){
    return obj1.age
  },
  set(v){
    obj1.age = v
    box.innerHTML = obj2.age
  }
})
input[1].oninput = function(){
  obj2.age=this.value
}
Object.defineProperty(obj2,'sex',{
  get(){
    return obj1.sex
  },
  set(v){
    obj1.sex = v
    box.innerHTML = obj2.sex
  }
})
input[2].oninput = function(){
  obj2.sex=this.value
}
 </script>        




# 六.数据劫持：（数据代理）VUE3.0   proxy
1.数据代理：通过一个对象代理另一个对象中属性的操作
<script>
const obj1 = {
  name : '张三',
  age : '男',
  sex : 24
}
const obj2 = new Proxy(obj1,{ //被代理对象
  get(obj2,shuxing){//参1：代理对象  参2：代理对象的属性
    return obj2[shuxing]//代理遍历，将所有的属性直接返回obj2->obj1,shuxing->name,age,sex
  },
  set(obj2,shuxing,value){//obj2->obj1,shuxing->name/age/sex,value就是设置的值
    obj2[shuxing] = value
  }
})
console.log(obj1)
console.log(obj2)
 </script>


2.数据代理input
<body> 
  <input type="text" class="input">
  <div class="box"></div>
</body>
</html>
</html>
<script>
const input = document.querySelector('.input')
const box = document.querySelector('.box')
const obj1 = {
  name : '张三',
  age : '男',
  sex : 24
}
const obj2 = new Proxy(obj1,{
  get(obj2,shuxing){
    return obj2[shuxing]
  },
  set(obj2,shuxing,value){
    obj2[shuxing] = value
    box.innerHTML = obj2.name
  }
})
input.oninput = function(){
  obj2.name = this.value 
}
console.log(obj1)
console.log(obj2)
 </script>













 <body> 
  <input type="text">
  <input type="text">
  <input type="text">
  <div class="box"></div>
</body>
</html>
</html>
<script>
const input= document.querySelectorAll('.input')
const box = document.querySelector('.box')
const obj1 = {
  name : '张三',
  age : '男',
  sex : 24
}
const obj2 = {}
Object.defineProperty(obj2,'name',{
  get(){
    return obj1.name
  },
  set(v){
    obj1.name = v
    box.innerHTML = input[0].value
  }
})
Object.defineProperty(obj2,'age',{
  get(){
    return obj1.age
  },set(v){
    obj1.age = v
  }
})
Object.defineProperty(obj2,'sex',{
  get(){
    return obj1.sex
  },set(v){
    obj1.sex = v
  }
})
obj2.name = '李四'
obj2.age = '女'
obj2.sex = '25'
console.log(obj1)
console.log(obj2)
input[0].oninput = function(){
  
}
 </script>   

            

