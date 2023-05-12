# 一.modules模块化

1. 作用：解决Vuex 的 Store 的代码臃肿

2. Vuex 允许我们将 Store 分割成 模块，每个模块都有自己的: stors/mutation/action/getter

3. 案例：

<script>
import Vue from 'vue'
import Vuex from 'vuex'
import { getHotList } from "@/api";//引入'axios'请求

Vue.use(Vuex)

//城市模块
const A = {
    state:() =>{
      ...
    },
    mutations: {
      ...
    },
    actions: {
      ...
    }
  }

//详情模块
const B = {
    state:() =>{
      ...
    },
    mutations: {
      ...
    },
    actions: {
      ...
    }
  }
}

//最受欢迎的模块
const C= {
    state:() =>{
      ...
    },
    mutations: {
      ...
    },
    actions: {
      ...
    }
  }
}

export default new Vuex.Store({
    modules:{
        a:A,
        b:B,
        c:C,
    }
})

4. 如果要分 modules 不同的模块名，则在组件中使用的时候，需要更改 计算属性() 的写法：
export default {
  computed:() {//以对象的形式
    ...mapState({
        list:(state) => state.a.list
    }),
  },
};
</script>

5. mutation/action/getter 则可以用数组的方法，除...mapState方法以外
<script>
  methods:{
    ...mapMutations(["changeCity"]),
  },



# 二.modules模块化：命名空间

1. namespaced:true  表示：命名空间的模块

2. 方法：
//城市模块
const A = {
    // 让A模块有命名空间
    namespaced:true 
    //没有加namespaced:true，stors/mutation/action/getter,在组件中使用的时候，不需要加{}，对象的方式，只有 state需要加属性名
    //加了 namespaced:true  ，则所有的属性在组件中使用的时候，都要加属性名

    state:() =>{
      ...
    },
    mutations: {
      ...
    },
    actions: {
      ...
  }
}

3. 没有加namespaced:true，stors/mutation/action/getter,在组件中使用的时候，不需要加{}，对象的方式，只有 state需要加属性名
<script>
export default {
  computed:() {//以对象的形式
    ...mapState({
        list:(state) => state.a.list
    }),
  },
  methods:{
    ...mapMutations(["changeCity"]),
  },
  methods:{
    ...mapActions(["getData"]),
    },
};

4. 加了 namespaced:true  ，则所有的属性在组件中使用的时候，都要加属性名
<script>
export default {
  computed:() {//以对象的形式
    ...mapState({
        list:(state) => state.a.list
    }),
  },
  methods:{
    ...mapMutations("a",["changeCity"]),
  },
  methods:{
    ...mapActions("b",["getData"]),
    },
};



# 三. 可以在Store文件夹中，建立不同的文件夹

1. 将每个modules模块，在Store文件夹中，再建立对应的modules文件夹，将其区分

2. 在对应的modules文件夹中，建立对应的js模块

3. 每个js模块，都要在Store文件中的index.js中注册：

import a from "./store/a";
import b from "./store/b";
import c from "./store/c";
export default new Vuex.Store({
    modules:{
        a:A,
        b:B,
        c:C,
    }
})

4. 每个js模块,将异步得到请求api引入

import { getHotList } from "@/api";

const A = {
    state:() =>{
      ...
    },
    mutations: {
      ...
    },
    actions: {
      ...
    }
  }
export default A  
// 暴露A的模块

