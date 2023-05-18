# 一.vue3 路由 

1. vuex 的 store
import { createStore } from 'vuex'

export default createStore({
  state: {
    count:10
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


2. 组件中
<template>
<div>{{ count }}</div>
</template>

<script lang="ts">
import { defineComponent,computed } from 'vue'//引入computed：计算属性
import { useStore } from "vuex"//引入useStore：vuex 的 store 的实例

export default defineComponent({
  setup() {

    const store = useStore()//store = vuex 的 store 的实例

    const count = computed(()=>{//利用computed：计算属性来获取，vuex 的 store 的实例 仓库的数据
      return store.state.count
    })

    return {
      count,
    }
  },
})
</script>


<style lang="less">

</style>
