# 一.组件添加v-model
1. 父组件的变量和子组件的input的值，做双向绑定

2. 组件上添加的任意事件，都是自定义事件

3. native 修饰符可以将组件的事件转为原生事件

  <body>
    <div id="app">
      <p>我时P标签:{{msg}}</p>
      <tb_father v-model="msg"></tb_father>
      <!-- 子组件绑定父组件的msg -->
    </div>
  </body>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    Vue.component('tb_father',{
      props:["value"],
      <!-- 因为父传子，需要props，value为：子组件的input的值和父组件的变量，做双向绑定 -->
      template:`
        <input type="text" :value="value" @input="fn">
            <!-- value为：input的值；；因为子传父，需要自定义事件来传参 -->
      `,
      methods:{
        fn(e){
          <!-- e为：input框-->
          this.$emit("input",e.target.value)
          <!-- this.$emit为：子传父参数的方法，参1为：事件本身，参2为：传递的input的value值 -->
        }
      }
    })
    const p1 = new Vue({
      el: "#app",
      data: {
        msg:123
        },
    },
   )
  </script>
</html>