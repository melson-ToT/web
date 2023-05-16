# 一.vue3 的路由

1. 安装 ：npm i vue-router@4

2. vue3 的路由引入：
<script>
 import { createRouter, createWebHashHistory } from 'vue-router'
 import HomeView from '../views/HomeView.vue'
 const routes = [
   {
     path: '/',
     redirect: '/home',
   },
  {
     path: '/home',
     component: () => import('../views/HomeView.vue')
   },
   {
     path: '/about',
     component: () => import('../views/AboutView.vue')
   }
 ]
 const router = createRouter({
  //哈希路由
   history: createWebHashHistory(),
   routes
 })
 export default router

4. 在 main.js 中去引入 router
import router from './router'
createApp(App)
.use(store).use(router).mount('#app')


# 二.如果是组件内部的跳转，

1. 则不能在 setup 中使用：thid.$router.push("/home"),

2. 在 setup 中访问路由
<template>
  <div @click="fn">点击这里</div>
</template>

<script>
import { useRouter,useRoute } from "vue.router";//引入路由
export default {
  setup() {

    //useRouter,useRoute 这两个函数，只能在 setup 的顶层执行

    //定义 router = 引入的路由
    const router = useRouter()

    //定义 router = 引入的路由信息
    const route = useRoute()

    //再将 router 代入到 fn的方法中
    const fn = () => {
      router.push("/home")
    };

    return {
      fn,
    };
  },
};
</script>

<style lang="less" scoped>
</style>



# 三.vue3 的vuex

1. vuex 的仓库:

<script>
 import { createStore } from 'vuex'
 export default createStore({
   state: {
    name:"zhangsan"
   },
   getters: {
   },
   mutations: {
   },
   actions: {
   },
   modules: {
   }
 })

2. 在main,js中引入：
<script>
import store from './store'
createApp(App)
.use(store).use(router).mount('#app')




#  三.组件中使用 vuex 的数据 name

<template>
  <div>{{ name }}</div>
</template>

<script>
import { computed } from 'vuex'  ----引用计算属性
import { useStore } from 'vuex'  ----引用 vuex 的 useStore才方法

export default {
  setup() {

    //仓库实例
    const stort = useStore()

    const name = computed(()=>{
      //获取 vuex 的 name
      return stort.name
    })

    return {
      name,
    };
  },
};

2. 如果在方法中华，想要改变 name
<script>
 import { createStore } from 'vuex'
 export default createStore({
   state: {
    name:"zhangsan"
   },

   mutations: {
    changename(state){
      state.name = "lisi"
    }
   },
 })

<template>
  <div><button @click="fn"></button> --{{ name }}</div>
</template>

<script>
import { useStore } from 'vuex'  ----引用 vuex 的 useStore才方法
export default {
  setup() 
    const name = computed(()=>{
      //获取 vuex 的 name
      return stort.name
    })

    //定义 stort = 仓库实例
    const stort = createStore()

    //再将 stort 代入到 fn的方法中
    const fn = () => {
      stort.commit("changename")
    };

    return {
      name,
      fn,
    };
  },
};

# 四.如果有 { useStore }，则不允许有 辅助函数








































