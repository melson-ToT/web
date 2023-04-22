# 一：单例模式
      一个构造函数一生只能new出一个对象
      当我们使用构造函数，每一次new出来对象的属性和方法完全一样的时候，我们就使用单例模式
      如果实例对象存在，直接返回，不存在，实例化再返回

1.把  let flag = null放在函数外部
<script>
let flag = true                              1.标记存在    8.当再点击时，标记为假
document.onclick = function(){               2.事件触发时
  if(flag){                                  3.如果标记存在
    const div = document.createElement('div')4.创建一个div
    div.innerHTML = 'hallo'                  5.内容为'hallo'
    document.body.appendChild(div)           6.追加到body
    flag = false                             7.标记为不存在
  }                                          
}
</script> 

2. 把  let flag = null放在函数内部,采用闭包的模式
<script>
class Fan{
  constructor(){
    this.div = document.createElement('div')
    document.body.appendChild(this.div)
  }
  init(text){
    this.div.innerHTML = text
  }
}
const son = function(){
  let flag = null
  return function(text){
    if(!flag){
      flag =  new Fan()
    }
    flag.init(text)
    return flag
  }
}()   
son('nihao')


# 二：组合模式：
         ----把几个构造函数的启动方式组合在一起
条件：
    1.创建几个class构造函数的方法
    2.重新创建一个class构造函数：包括1个属性和2个方法
    3.属性1:穿件一个空数组，方法1，之前创建的方法push到这个方法中去，方法2.来遍历这个数组
    4.执行这个class构造函数
<script>
class Fa{
  init(){
    console.log('1111');
  }
}
class Fb{
  init(){
    console.log('2222');
  }
}
class Fc{
  init(){
    console.log('3333'); 
  }
}                            1.用构造函数创建Fa.init/Fb.init/Fc.init,事件处理函数3个方法
class FF{                    2.重新创建一个构造函数
  constructor(){                 （2.1）构造函数，属性为：数组
    this.zuhe = []
  }
  add(obj){                      （2.2）方法:把之前的3个构造函数的方法push到FF.add内，obj是形参
    this.zuhe.push(obj)
  }
  emit(){                        （2.3）方法：对this.zuhe的数组进行遍历
    this.zuhe.forEach(item=> item.init())
  }
}
let p1 = new FF()           3.FF的实例对象
p1.add(new Fa)              4.把需要一起操作的方法push到new FF()内
p1.add(new Fb)
p1.add(new Fc)
p1.emit()                   5.执行new FF()组合内的遍历
</script> 


# 三.发布订阅模式:
                ----观察者模式
                ----消息者模式
  定义：当一个对象的状态发生改变时，所有依赖于他的对象都会得到通知，解决了主体对象与消息者之间功能的耦合
    即：当一个对象的状态发生改变时，给其他对象通知的问题

条件:
  1.在构造函数的属性内，创建一个空数组
  2.在构造函数的方法内，创建几个方法：
                                 添加
                                 执行
                                 删除

# 事件都是由时间处理函数来处理的
<script>
function F1(){
    console.log('买白菜');
  }
function F2(){
    console.log('买青菜');
  }
function F3(){
    console.log('买宝马');
  }
function F4(){
    console.log('买奥迪');
  }
function F5(){
    console.log('买平房');
  }
function F6(){
    console.log('买楼房');
  }
class FF{
  constructor(){
    this.zuhe = []
  }
  add(obj,fn){
    if(!this.zuhe[obj]){
      this.zuhe[obj]=[fn]
    }else{
      this.zuhe[obj].push(fn)
    }
  }
  emit(obj){
    if(!this.zuhe[obj]){
      return
    }else{
      this.zuhe[obj].forEach(item=> item())
    }
  }
  del(obj,fn){
    for(let i=0;i<this.zuhe[obj].length;i++){
      if(this.zuhe[obj][i]===fn){
        this.zuhe[obj].splice(i,1)
      }
    }
  }
}
let p1 = new FF()
p1.add('买菜',F1())
p1.add('买菜',F2())
p1.add('买菜',F3())
p1.emit()
p1.del('买菜',F2())
</script> 

  
  
