# 一.过渡的概述
1. 在css过渡和动画中自动应用class
2. 可以配合使用第三方长沙市动画库，如Animate.css--https://animate.style/
3. 在过渡钩子函数中使用JavaScript直接操作DOM
4. 可以配合使用第三方JavaScript动画库，如Velocity.js


# 二.过渡的类名

1. v-enter:进入过渡的开始状态

2. v-enter-active:进入过渡生效时的状态

3. v-leave-active:离开过渡生效时的状态

4. v-leave-to：离开过渡的结束状态


# 三.单元素/组件的过渡
Vue提供了 transition 的封装组件，可以给任何元素和组件添加进入/离开的过渡

1. 条件渲染 v-if

2. 条件展示 v-show

3. 没有进行过渡的，只显示元素的出现和消失
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


# 四.单元素/组件的过渡----方法（实现元素淡入淡出）

1. 在v-if外面套一个 <transition>的标签

2. 在<transition>标签名上加name属性 <transition name="sss"> 

3. 在<style>内写：

<style>
  .sss-enter-active,.sss-leave-active {
    /* 进入前的过程     离开后的过程 */
    transition: opacity 0.5s;
  }
  .sss-enter,.sss-leave-to {
    /* 进入前     离开后 */
    opacity : 0
  }
</style>
<body>
  <div id="app">
    <button @click="show=!show">按钮</button>
    <transition name="sss">
      <p v-if="show">过渡</p>
    <transition>
    <!-- 给v-if或者x-show的元素添加transition的标签，里面需要name属性 -->
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


# 五.实现元素淡入淡出的显示和消失
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


# 六.实现元素CSS动画
     和过渡的写法一直，其他的参照css的写法


# 七.过渡的类名----与第三方引入

(一)：enter-active-class=""进入的动画

(二)：leave-active-class=""离开的动画

(三)：enter-class=""

(四)：leave-class=""

(五)：enter-to-class=""

(六)：leave-to-class=""



进入的动画：

1. 百度，输入bootcnd，点击(BootCDN - Bootstrap 中文网开源项目免费 CDN 加速服务)
2. 输入Animate.css，点击下方的Animate.css
3. 点击  </>复制<link>标签
4. 在  <title>Document</title>下方直接粘贴
5. 在写好的<transition>标签上加enter-active-class=""
6. 打开 https://animate.style/，找到对应的效果 ，在<h1 class="animate__animated animate__bounce"></h1> 中复制 class中的animate__animated animate__bounce，
7. 粘贴到<transition>标签的enter-active-class=""中
8. 在https://animate.style/ 对应的效果后面，点击方块，
9. 再将<transition name="sss" enter-active-class="animate__animated animate__bounce">的后半截删除，将在https://animate.style/ 对应的效果后面，点击方块，复制到里面去<transition name="sss" enter-active-class="animate__animated animate__lightSpeedInLeft">

出去的动画也是一样的
1. 因为在Animate.css内，已经引入了，所以前4部分省略，
2. 在<transition>标签上继续写：leave-active-class=""
3. 打开 https://animate.style/，找到对应的效果 
4. <h1 class="animate__animated animate__bounce"></h1> 中复制 class中的animate__animated animate__bounce，
5. 粘贴到在leave-active-class=""内，
6. 在https://animate.style/ 对应的效果后面，点击方块，
7. leave-active-class="animate__animated animate__bounce"的后半截替换为，刚才在https://animate.style/ 对应的效果，Ctrl+V即可


案例：：
<style>
  .sss-enter-active, .sss-leave-active {
    transition: all 1s;
  }
  .sss-enter {
    
    opacity : 0
  }
 .sss-leave-to {
   
    opacity : 0
  }
</style>
<body>
  <div id="app">
    <button @click="show=!show">按钮</button>
    <transition name="sss" 
    enter-active-class="animate__animated animate__lightSpeedInLeft" 
    leave-active-class="animate__animated animate__lightSpeedOutRight">
      <p v-if="show">过渡的样式你要怎么定</p>
    </transition>
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



