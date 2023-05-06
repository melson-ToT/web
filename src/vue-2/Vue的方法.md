# 一.vue 概述：

1. 官网：https://cn.vuejs.org/

2. vue.js 的在线引用地址(vue 官方引入地址)：
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>

3. nasa20004811gmail.com

4. 全局查找文件：Ctrl+p

5. 单个文件查找 文字或字母：Ctrl+f

6. 删除相应vue全家桶代码的严格模式：npm uninstall 对应的文件


# 二.代码：

### 自定义属性如果是变量的话，前面一定要加：号
  如：  <p :name="item.name"><p>

1. el:表示要控制那个元素，是element的简写，

2. data:变量响应式数据（数据驱动视图）但是放在子组件中，只能使用函数返回对象

3. methods:事件处理函数（对象）

4. template:组件里面写html的内容

5. components:注册局部组件的

6. v-for（=）循环，遍历list每一项(item)      

7. v-if（=）：条件渲染, {v-if:如果，v-else-if:或者，v-else:则是}

8. v-model（=）：是变量和input的值做双向绑定

9. v-bind（:）：添加和绑定标签的属性，
             如：<p v-bind:class="{font:show}"></p>简写为：<p :class="{font:show}"></p>

10. v-on（:）:事件处理，如v-on：click=''  或@click=''

11. computed：{}    计算属性-固定写法

12. v-html=""将data内的如：<p v-thml="ccc">我是p标签</p>，改为：我是p标签

      案例：
      <p v-thml="ccc">我是p标签</p>
      ccc:<p>我是p标签</p>

13. v-text="",将data内的数据，当成字符串进行渲染

14. 如果在一个标签内加title属性，鼠标移入进去时，就可以看见提示文字了
       <p title="中国好声音">我是p标签</p>，
        鼠标移入进去时，就可以看见：  中国好声音

15. placeholder是input的提示文字<input placeholder="提示文字"/>

16. props:用于子组件接收父组件的自定义属性["数组类型"]

17. v-slot:"",具名插槽的方法

18. name:""的方法，给template标签进行声明，递归组件，自己调自己用的


# 三.VUE提供的标签：
<template></template>：占位符
<component></component>：动态组件标签
<slot></slot> 插槽
<heep-alive></heep-alive>缓存组件


# 四.两个生命周期： 一般在定时器的外部使用，同于缓存组件
1. activated(){}:
        被<keep-alive>缓存的组件激活时调用

2.deactivatde(){}
        被<keep-alive>缓存的组件失活时调用



# 四.动态参数：
  1.submit 是自动刷新页面的功能


# 五.获取DOM元素
<div id="app">
  <input type="text" ref="www">
</div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  new Vue({
    el: "#app",
    data: {
    },
    mounted(){
      this.$refs.www
    },
  })
</script>
</html>


# 六.下拉菜单三级联动------递归组件方法

1. 给子组件自定义属性，来获取父组件data中的list

2. 在父组件内注册子组件的名称

3. 利用v-for来获取对应的响应式数据

4. 用 name:"Ai"的方法，给<Ai>标签进行声明，递归组件，自己调自己用的

5. 在template内的<Ai>标签内，编辑父组件data中的item的children，都是在v-for内，所以和title一样遍历

6. 在template内的<Ai>标签内，加v-if="item.children"防止溢出


<div id="app">
  <Ai :list="list"></Ai>
</div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const Ai = {
    name:"Ai",//因为template内的<Ai>标签还没有声明，要想在内部使用，就必须用name，给它一个名字 
    props:["list"],
    template: `
     <ul>
      <li v-for="item in list" :key="item.title">
        {{item.title}}
        <Ai :list="item.children" v-if="item.children"></Ai>   
                                 //  v-if="item.children"防止溢出
      </li>
    </ul>
   `
  }
  new Vue({
    el: "#app",
    data: {
      list: [
        {
          title: '江苏省',
          children: [
            {
              title:'南京市',
              children:[
                {
                  title:'111街道'
                },
                {
                  title:'222街道'
                },
                {
                  title:'333街道'
                },
              ]
            },
            {
              title:'无锡市',
              children:[
                {
                  title:'444街道'
                },
                {
                  title:'555街道'
                },
                {
                  title:'666街道'
                },
              ]
            },
            
          ]
        },{
          title: '安徽省',
          children: [
            {
              title:'南京市',
              children:[
                {
                  title:'777街道'
                },
                {
                  title:'888街道'
                },
                {
                  title:'999街道'
                },
              ]
            },
            {
              title:'无锡市',
              children:[
                {
                  title:'101街道'
                },
                {
                  title:'102街道'
                },
                {
                  title:'103街道'
                },
              ]
            },
            
          ]
        }
      ]
    },
    components: {
    Ai
  }
  })
</script>
</html>


# 七.点击按钮，显示元素出现和消失
<body>
  <div id="app">
    <button @click="show=!show">按钮</button>
    <p v-if="show">过渡</p>

  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  new Vue({
    el:"#app",
    data:{
      show:true
    }
  })
</script>
</html>


# 八.实现元素淡入淡出的显示和消失
<style>
  .sss-enter-active, .sss-leave-active {
    transition: all 1s;
    /* 元素的进入前和离开后，都是过渡时间为1秒 */
  }
  .sss-enter {
    transform: translateX(50px);
    opacity : 0
    /* 元素进入前向右平移50px */
  }
  .sss-enter,.sss-leave-to {
    transform: translateX(-50px);
    opacity : 0
    /* 元素离开后向左平移50px */
  }
</style>
<body>
  <div id="app">
    <button @click="show=!show">按钮</button>
            <!-- 点击取反 -->
    <transition name="sss">
      <p v-if="show">过渡</p>
    <transition>
    <!-- 如果show存在，否则消失 -->
  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  new Vue({
    el:"#app",
    data:{
      show:true //布尔值
    }
  })
</script>
</html>


# 九.过渡的网址和引入的地址
1. 过渡的动画库网址：https://animate.style/ 
2. 过渡动画的引入地址： bootcnd，点击(BootCDN - Bootstrap 中文网开源项目免费 CDN 加速服务)


# 四.商品列表：
  </body>
</html>
<body>
   <div id="app">
      <p>{{msg}}</p>     
      <!-- 1.vue的js变量带入 -->
      <ul>
         <li v-for="item in list">      
          <!-- 2.js的list内，数组的v-for循环，遍历list每一项(item) -->
            {{item.product_name}}的库存还剩{{item.count}}件 - 
            <!-- 3.list每一项(item)的product_name
            4.list每一项(item)的item.count -->

            <span v-if="item.count === 0">卖完了</span>
            5.v-if：条件渲染。当 ===0，则显示 span标签

            <input type="number" v-model="item.count">
            6.v-model是变量和input的值做双向绑定
         </li>
      </ul>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
   <script>
      let p1 =new Vue({
         //引入的vue是一个构造函数，如果要使用，就要去生成一个实例对象
         //里面需要一个对象做参数key,value
         //里面的key:有个专门的名称option（选项的意思）
         el: "#app",
         //el:是element的简写，el表示可以去控制那个元素，那么这个元素内的元素和内容就可以被vue控制
         data: {
            //data:变量（响应式数据），当数据改变，页面就跟着改变：数据驱动视图
            msg: "hello Vue!",//对应body的msg变量
            list: [
               {
                 product_name:'衣服',
                 count:5
               },
               {
                 product_name:'鞋子',
                 count:0
               },
               {
                 product_name:'包包',
                 count:8
               },
            ]
         },
         computed:{//计算属性-固定写法computed
            total(){//写的函数，并返回一个值，根据计算的数据，去计算得到一个新的值
               return this.list.reduce((sum,item)=>{
                //返回  p1.list   reduce累加：固定写法
                  return (sum += +item.count);
                  //返回  reduce累加（数量=所有的count）+代表：数字的意思
               },0)//从0开始累加
            },
         },
      });
   </script>
</body>
</html>


# 五.图片的懒加载
<body>
   <div id="app">
      <button v-on:click="attr='src'">按钮</button> 
      <img v-bind:[attr]="url" alt="">
   </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
   const p1 = new Vue({
      el: '#app',
      data: {
         attr:'data-src',
         url:'https://img0.baidu.com/it/u=3251444720,2087998293&fm=253&app=138&size=w931&n=0&f=BMP&fmt=auto?sec=1681318800&t=a45ab062abdee5bbf570eb5795c58ff2'
      },
   })
</script>
</html>


# 六.本地存储
        1. 本地存储：Session Storage(强制刷新或关闭页面，存储的数据自动丢失)
        2. 本地存储：Local Storage(强制刷新或关闭页面，存储的数据自动丢失)
        3. 本地存储：Cookise(第二个值必须填写保留的时间)
