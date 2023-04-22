# 一.props的传递
    子组件接收父组件传过来的自定义属性

1. 如果值是固定值：<Child age="20"></Child>，则不用加：号

2. 如果是值是变量或表达式的：<Child :age="num"></Child>，则必须加：号

3. 如<Child :age="20"></Child>，加：号，就是表达式，代表20为表达式

4. 如<Child :age="'20'"></Child>，加：号，'20'，就是字符串

5. props：{
      name:String,   字符串
      mag:Number     数字
      list:Array     数组
      obj：Object    对象
    }

6. props接收的可以使用数组或对象类型的
#  优点：可以规定用户传来的数据类型
props: ["name","age","sax"]

props: {
      name:String,
      age:String,
      mag:Number
    },


# 二.案例：子组件用props对象的形式接收父组件传来的数据
<body>
  <div id="app">
    <Child :name="name" :age="age" :mag="mag"></Child>
  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const Child = {
    props: {   //可以约定用户(在input框)的输入的数据类型
      name:String,
      age:String,
      mag:Number
    },
    template: `<li>{{name}}-{{age}}-{{mag}}</li>`,
  }
  new Vue({
    el: '#app',
    data: {
      name: 'zhangsan',
      age:'男',
      mag:20
    },
    components: {
      Child
    }
  })
</script>
</html>


# 三.单向数据流
1. Vue是单向数据流
2. 所有的父级元素只会传递给子元素，而子元素不会给父元素，防止子元素变更时，影响父元素的状态
3. 如果是父传子，子组件里面是不能去修改props的值，不然就会报错
4. 只能父组件去改变子组件，子组件不能改变父组件，也不能影响父组件，不然就会报错
5. 子传父，是不会影响单向数据流
6. 双向数据绑定是：input的内容绑定变量，也是不会影响单向数据流


# 四.改变单向数据流
     父传子，如果子组件确实想改变父组件的数据，可以让子组件把父组件传递过来的数据存一下，再使用：
<body>
  <div id="app">
    <h3>{{name}}</h3>
    <!-- 父组件直接使用 -->
    <button @click="name++">点击按钮</button>
    <!-- 父组件的点击 -->
    <Child :name="name"></Child>
    <!-- 子组件，用自定义属性来接收父组件的值 -->
  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const Child = {
    data(){
      return {
        num:this.name  //用data的方法来存一下父组件传来的值，此时父组件的数据，就会变成子组件的初始值，父组件与子组件失去响应式
      }
    },
    props: {          //这里的只能用name来接收，用num则无法识别父组件的数据
      name:Number,    //用 props来接收存父组件的数据
    },
    template: `<li>{{num}}-<button @click="num++">点击按钮</button></li>`,
               //用data改变的变量来使用
  }
  new Vue({
    el: '#app',
    data: {
      name: 20,  //父组件的变量
    },
    components: {
      Child
    }
  })
</script>
</html>



# 五.props的验证

1. props--类型验证

   props：{
      name:String,   字符串
      mag:Number     数字
      list:Array     数组
      obj：Object    对象
    }


2. props--双向类型验证
   props: {
      name:[Number,String],   数字或字符串
      age:[Number,Array]      数字或数组
    },


3. props--必填验证
<!-- 如果父组件的age为空 或 子组件标签没有age为空，则报错-->
<!-- required:true  必填 -->

    <Child :name="name" :age="age"></Child>
    props: {
      name:String,
      age:{
        type:Number,
        <!-- type为：数据类型 -->
        required:true  
        <!--  required：必填 -->
      }
    },
    template: `<li>{{name}}-{{age}}</li>`,
  }
  new Vue({
    data: {
      name: 'zhangsan',
      age:'20'
    },


4. props--默认值验证
<!-- default:5000  默认值为5000 -->

如果这只一个默认值，则在Child子标签内不能设置mag，直接不写
    <Child :name="name" :age="age"></Child>
    props: {
      name:String,
      age:{
        type:Number,
        required:true
      },
      mag:{
        type:Number,
        default:5000
      }
    },
    template: `<li>{{name}}-{{age}}-{{mag}}</li>`,
  }
  new Vue({
    el: '#app',
    data: {
      name: 'zhangsan',
      age:20,


5.props--符合条件验证--validator叫做自定义验证函数，里面需要return true或false
<!-- height:{
       validator(value){  //validator叫做自定义验证函数，里面需要return true或false
          return value > 170
        }
} -->

<body>
  <div id="app">
    <Child :height="height"></Child>
  </div>
</body>
<script>
  const Child = {
    props: {
      height:{
        validator(value){//validator叫做自定义验证函数，里面需要return true或false
          return value > 170
        }
      }
    },
    template: `<li>{{height}}</li>`,
  }
  new Vue({
    el: '#app',
    data: {
      height:180
    },
    components: {
      Child
    }
  })
</script>
</html>



