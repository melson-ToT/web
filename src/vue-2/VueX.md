# 一.VueX的概述

1. VueX是Vue程序开发的状态管理模式

2. state:驱动应用的数据源

3. view:以声明方式将state映射到视图

4. actions：响应在view上的用户输入导致的状态变化

5. 将data的count的数据放在state的仓库内，如果那个组件需要数据，可以直接在VueX的state的仓库内调用

6. 当count的数据改变时，其他组件的数据也跟着改变



# 二.VueX的流程

1. 组件 -> 通过触发 -> actions(异步函数) -> 通过提交 -> mutations(同步函数) -> 通过改变 -> 全局的状态改变 -> 组件重新渲染

2. 后端的api接口 -> actions(异步函数)



# 二.什么时候使用VueX

1. VueX可以帮助我们管理共享状态

2. VueX是大型单页面应用

3. 在VueX在组件外声明变量



# 三.VueX安装

1. npm i vuex

2. 在main,js中引入：
<script>
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
//import store from "./store";
import css from "./views/css.css"
import "./assets/font_k1hyk6b1km/iconfont.css"

Vue.config.productionTip = false;

new Vue({
  router,
  //store,
  render: (h) => h(App),
}).$mount("#app");

3. 在src中建立一个store文件夹，在文件夹建立一个store.js的文件

4. 在store.js的文件中引入：

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)//使用Vuex的插件

//创建仓库的实例并暴露
export default new Vuex.Store({
    state: {
      count:10,
      //state对象里面写的：全局的变量,组件可以调用
    },
    getters:{
      //
    },
    mutations: {
      
    },
    actions: {
     
    },
    modules:{

    }
})


# 四.组件调用VueX的store中的count,----当仓库数据改变时，组件内的数据跟着改变

1. 在对应的组件内//这种方法是错误的，只能通过计算属性
data(){
  return {
    count:this.$store.store.count
    //     this.$store是Vuex.Store实例对象 ->下的：state: {count:10},
  }
}

2. 在标签中使用
<template>
  <div>
    <p>{{count}}</p>
  </div>
</template>


3. 不能直接在 data(){return {count:this.$store.store.count}}使用count，因为这样就没有响应式，

4. 如果仓库的count数据改变，但组件内的count不会改变

5. 只能通过计算属性：

computed:{
  count(){
    return this.$store.store.count
  }
}

6. 因为 data()内的数据是一个初始值
  data(){
    return {
      count:this.$store.store.count
    }
  }

7. 获取Vuex.store仓库的数据，只能通过计算属性获取



# 四.VueX(仓库数据改变，组件跟着改变)--一个变量多个组件使用

案例：一个store仓库的数据可以给多个组件使用

1. 父组件
<template>
  <div>
    <HomeHeader />
    <HomeFooter />
  </div>
</template>

<script>
import HomeHeader from "./HomeHeader.vue";
import HomeFooter from "./HomeFooter.vue";
export default {
  components: {
    HomeHeader,
    HomeFooter,
  },
};
</script>

2. 子组件：---->只能通过计算属性
<template>
  <div>
    <p>{{count}}</p>
    <!-- 接收计算属性的count-->
  </div>
</template>

<script>
export default {
  computed:{
  count(){
    return this.$store.store.count//可以接收store仓库的数据
  }
}
},

3. store.js的文件
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)//使用Vuex的插件

//创建仓库的实例并暴露
export default new Vuex.Store({
    state: {
      count:10,
      //state对象里面写的：全局的变量,组件可以调用(一个变量多个组件使用)
    },
    getters:{
      //
    },
    mutations: {
      //放函数，是唯一可以改变state仓库的地方
    },
    actions: {
     
    },
    modules:{

    }
})



# 五.VueX----多个组件都去改变同一个状态

1. 给组件添加点击事件
<template>
  <div>
    <button @click="fn">点击事件</button>
  </div>
</template>

<script>
export default {
  computed:{//这里是：state仓库改变值改变，组件的值跟着改变
    count(){
      return this.$store.store.count
    }
  },
  methods:{//这里是：组件改变值改变，（多个组件都去改变同一个状态）
    fn(){
      this.$store.commit("add")
    }
  }
}
</script>

2. 在state仓库中 mutations：{}内，写方法
<script>
export default new Vuex.Store({
    state: {
      count:10,
      //state对象里面写的：全局的变量,组件可以调用
    },
    mutations: {
      add(state){
        state.count++
      }
    },
})



# 六.VueX 的 state

1. state就是存储全局数据的地方

2. VueX里只能有state这一个数据的仓库

3. 组件中只能通过计算属性，的 return this.$store.的某项值来获取 state仓库的值

4. 这样就形成可响应式数据，当state仓库的数据改变时，组件中的数据也会改变

5. mapState辅助函数，作用：当组件获取多个state仓库的数据时，可以通过 mapState 进行简化写法
案例：
(1).state仓库:
export default new Vuex.Store({
    state: {
      count:10,
      mame:"张非"，
      age:35,
    },

(2).组件获取：
<template>
  <div>
    {{count}}-{{mame}}-{{age}}
  </div>
</template>

<script>
import {mapState} from "VueX"//引入mapState辅助函数
export default {
  computed:mapState(["count","mame","age"]),//在计算属性内，利用mapState辅助函数，进行简写数据
}
</script>

6. 利用 mapState辅助函数，数组的方法的缺点：

(1). 当组件的data()中，与state仓库里，有相同的属性名，并调用时，会有冲突

(2).解决办法：对象的方式：
<script>
export default {
  data(){
    return {
      name:"lisi"//已有name 
    }
  },
  computed:mapState(){
    count："count",
    mame2："mame",   //mame2自己定义的，mame2 = 是state仓库的name,不会与data()的name冲突
    age："age"
   }
}

<template>
  <div>
    {{count}}-{{mame2}}-{{age}}
  </div>
</template>

(3).函数式写法
  computed:mapState(){
    count："count",
    mame2："mame", 
    age：(state) => state.age
   }

(4).如果想与组件中：data()的name数据进行拼接，则不能使用箭头函数的写法，因为 this的指向错误

案例1：
     错误（在箭头函数中，this的指向函数本身）
  computed:mapState(){
    count："count",
    mame2："mame", 
    age：(state) => state.age + this.mame//data()的name
   }

案例2：
     正确（普通函数，this的指向：data()的name）--谁调用指向谁
  computed:mapState(){
    count："count",
    mame2："mame", 
    age：(state) {
      return state.age + this.mame //普通函数加：return
    } 
  }

7. 如果组件中有多个计算属性，则可以通过对象的{...mapState}
computed:{
  ...mapState(){//多个计算属性,前面加...mapState
    count："count",
    mame2："mame", 
    age：(state) => state.age + this.mame//data()的name
  },
  fn(){////最后一个计算属性,不用加...
    return this.count * 2
  }
}



# 七.VueX 的 mutations

1. 放函数，是唯一可以改变state仓库的地方

2. payload:提交载荷--传参数

3. payload只允许有一个参数，多个参数时，以对象的形式传参，哪怕你的对象只有一个值
案例：
(1).组件：
<template>
  <div>
    <button -{{count}}- @click="fn">点击事件</button>
  </div>
</template>

<script>
export default {
  methods:{
    fn(){
      this.$store.commit("add",{num:3})
    }
  }
}

(2)state仓库
export default new Vuex.Store({
    state: {
      count:10,
    },
    mutations: {
      add(state,{payload}){
        state.count += payload.num
      }
    },
})

4. 使用 mutations 的 payload 在组件的方法中，简洁写法：
<template>
  <div>
    <button -{{count}}- @click="fn">点击事件</button>
  </div>
</template>

<script>
export default {
  methods:{
    fn(){
      this.$store.commit{//以对象的形式
        type:"add",
        num:3
      })
    }
  }
}

5. mutations 必须是同步函数
(1). 因为开发工具的记录，是在 mutations函数触发的时候生成的，而不是在数据改变的时候生成的
(2). 如果有异步的函数，则放在actions函数内
(3). mutations 放同步函数，actions 放异步函数

6. 在组件中提交多个 mutations
(1).正常写法
<template>
  <div>
    <button -{{count}}- @click="fn1">点击事件</button>
    <button -{{count}}- @click="fn2">点击事件</button>
  </div>
</template>

<script>
export default {
  methods:{
    fn1(){
      this.$store.commit("add",{num:3})
    },
    fn2(){
      this.$store.commit("minus",{num:3})
    },
  }
}

//state仓库
export default {
    mutations: {
      add(state,{payload}){//add加的意思--自定义的
        state.count += payload.num
      },
      minus(state,{payload}){//minus减的意思--自定义的
        state.count -= payload.num
      },
    },


(2).利用 mapmutations 进行简写:
1.在组件中引入：import {mapmutations} from "VueX"//引入mapmutations辅助函数
1.在组件中引入：
   
<template>
  <div>
    <button  -{{count}}- @click="fn1">点击事件</button>
    <button  -{{count}}- @click="fn2">点击事件</button>
  </div>
</template>

<script>
export default {
  methods:{
    ...mapMutations(["add","minus"])//将仓库的 mutations函数，映射到组件中
    fn1(){
      this.add({num:3})
    },
    fn2(){
      this.minus({num:3})
    },
  }
}

//state仓库
export default {
    mutations: {
      add(state,{payload}){//add加的意思--自定义的
        state.count += payload.num
      },
      minus(state,{payload}){//minus减的意思--自定义的
        state.count -= payload.num
      },
    },



# 八.VueX 的 actions

1. actions函数 类似于 mutations函数

2. actions函数是不能修改 state内的数据

3. actions函数只能提交 mutations函数
<template>
  <div>
    <button -{{count}}- @click="fn">点击事件</button>
  </div>
</template>

<script>
export default {
  computed:{//这里是：state仓库改变值改变，组件的值跟着改变
    count(){
      return this.$store.store.count
    }
  },
  methods:{//这里是：组件改变值改变，（多个组件都去改变同一个状态）
    fn(){
      // 使用dispatch去触发 actions 的函数
      this.$store.dispatch("addAsync")
    }
  }
}

//state仓库
export default {
    mutations: {
      add(state,{payload}){//add加的意思--自定义的
        state.count += payload.num
      },
      minus(state,{payload}){//minus减的意思--自定义的
        state.count -= payload.num
      },
    },
    actions：{//actions 里面也是函数，不能去改变 state ，只能去提交 mutations
      addAsync(context){//允许接收 context：可以接受 mutations 内部的 add
        setTimeout(()=>{
          context.commit("add",{num:3})
        },2000)
      }
    }

4. 如果 mutations 里面如果要作异步操作，是不可以的，必须通过 actions 内做异步来触发

5. actions 通过 context.commit 来获取 mutations 的 add

6. 组件再通过： methods方法来获取 mutations 的 add
  computed:{//这里是：state仓库改变值改变，组件的值跟着改变
    fn(){
      this.$store.commit("add")
    }
  },

7. 如果组件要获取 store仓库 内的 多个值，需要在组件内引入 mapState 的方法

(1).组件
<template>
  <div>
    {{count}}-{{mame2}}-{{age}}
  </div>
</template>

<script>
import {mapState} from "VueX"

export default {
  computed:{
    ...mapState(["count","mame","age"]),//在计算属性内，利用mapState辅助函数，进行简写数据
  }
}

(2).store仓库
export default new Vuex.Store({
    state: {
      count:10,
      mame:"张非"，
      age:35,
    },
})

8. 利用 mapActions 进行简写:如果 actions 多个异步的方法，需要在组件内引入 mapState 的方法
(1).在组件中引入
import { mapActions } from "VueX"

(2).在组件内方法中使用
export default {
  methods:{
    ...mapActions(["addAsync","a","b"]),//在计算属性内，利用mapState辅助函数，进行简写数据
    // 多个actions 的异步方法
  }
}



# 九.VueX 的 getters：
// 相当于 VueX 的计算属性
// 先将数组在 VueX 的 getters 中，计算好，再在组件中属于

(1). store仓库
export default new Vuex.Store({
    state: {
      count:[1,2,3,4,5,6,7,8,9]
    },
})

(2). getters 先将 count
getters：{
  addlist(state){  //addlist(state,getters)   getters可以依赖state的变量，页可以依赖其他的getters
    return state.count.filter((item =>item % 2))
                      // 过滤(偶数)
  }
}

(3). 组件中引入 getters
import { getters } from "VueX"

(4). 也是用计算属性
export default {
  computed:{
    list(){
      return this.$state.getters.addlist
    }
  }
}

(5). 组件的 html
<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item"></li>
    </ul>
  </div>
</template>



# 十.猫眼电影的案例

思路：
    城市.点击进入 -> Vuex.Store的 mutations -> mutations获取state数据 -> 城市选择 -> 城市选择页面的计算方法 -> 等于Vuex.Store 的 mutations 的值-> 点击对应的城市 -> 通过计算属性 -> 获取Vuex.Store 的 state.城市，并显示到页面 -> 

1. store仓库
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
    state: {
      cityName:"北京",
      cityId:1002,
    },
    mutations: {
      changeCity(state,payload){
        state.cityName = payload.name //state的cityName = payload形参.name是自定义的
        state.cityId = payload.id //state的cityId = payload形参.id是自定义的
      }
    },
    actions: {
      
    }
})

2. 组件
<template>
  <div class="Tab">
    <span class="uspan" @click="Gotcity">{{cityName}}</span>
                                         // 接受计算属性的 cityName()方法
<script>
export default {

  computed:{
    cityName(){
      return this.$store.state.cityName
    }
  },
</script>

3. 城市选择页面中，计算方法
<script>
import { mapMutations} from "vuex";
export default {
  methods:{
    ...mapMutations(["changeCity"]),//引入mutations 的 changeCity方法
    getcity(item){//上面共用一个事件，（item，val），此时的item是形参
      this.changeCity({name:item.name,id:item.cityId})//store仓库的 mutations 方法，name是payload.name,id是payload.id
      localStorage.setItem("name",item.name)//当再次登录时，就是上次点击的城市
      localStorage.setItem("id",item.cityId)
      this.$router.go(-1)//点击时，后退一步
    }
  }
}


