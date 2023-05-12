# 一.将“城市选择页面”数据请求放在VueX中

1.将数据接口，放在VueX中请求
<script>
import Vue from 'vue'
import Vuex from 'vuex'
import { getHotList } from "@/api";//引入'axios'请求

Vue.use(Vuex)

export default new Vuex.Store({
    state: {
      cityName:localStorage.getItem("name") || "北京", //将最后的城市选择，存储到本地：当再次登录时，就是上次点击的城市
      cityId:localStorage.getItem("id") || 1002,       //setItem:是存，getItem：是取，||:如果没有存储过，则默认是："北京",1002,

      // 数据也要放在VueX中
      list:[],
    },
    mutations: {
      changeCity(state,payload){
        state.cityName = payload.name //state的cityName = payload形参.name是自定义的
        state.cityId = payload.id //state的cityId = payload形参.id是自定义的
      },
      getHotState(state,payload){//因为不可以直接获取 state中的 list:[]，需要在 mutations设置方法，并传值
                    // payload = actions 中 getHot内的res
        state.list = payload.data.data.not
      }
    },
    actions: {//将异步的请求数据放在actions中
      getHot({commit}){//传入 mutations 中 {commit}的解构方法，将 actions 中获取的异步数据，传给 mutations
        getHotList().then((res) => {
          // this.list = res.data.data.not ----是不可以直接获取 state中的 list:[]
          commit("getHotState",res)
          //commit 传给 mutations 的 getHotState方法，   res = payload
        })
      }
      //或 async 和 await
      async getHot({commit}){
        const res = await getHotList()
        // this.list = res.data.data.not ----是不可以直接获取 state中的 list:[]
        commit("getHotState",res)
      }
    }
})

2. 在组件中通过计算属性获取：Store仓库actions中的异步方法

<template>
  <div class="father" v-if="list.length">
    <div class="not-city">
      <p>热门城市</p>
      <div class="not-diqu" v-for="item in hotCity.cities" :key="item.cityId" @click="getcity(item)">
        {{ item.name }}
      </div>
    </div>
    <div class="city" v-for="(item, index) in otherCity" :key="index">
      <p>{{ item.title }}</p>
      <div class="diqu" v-for="val in item.cities" :key="val.cityId" @click="getcity(val)">
        {{ val.name }}
      </div>
    </div>
  </div>
</template>

<script>
删除，import { getHotList } from "@/api"; 因为直接在 Store仓库的 actions 中请求数据，所以不需要在组件中引入了
import { mapState,mapMutations，mapActions} from "vuex";

export default {
  mounted(){//将 actions 的方法引入到生命周期
    this.$store.dispatch("getHot")，//Store仓库actions中的异步方法   ...mapState(["list"])//获取state 的 list
  },
  methods:{
    ...mapMutations(["changeCity"]),//引入Store仓库中 mutations方法
    getcity(item){//上面共用一个事件，（item，val），此时的item是形参
      this.changeCity({name:item.name,id:item.cityId})//store仓库的 mutations 方法，name是payload.name,id是payload.id
      localStorage.setItem("name",item.name)//当再次登录时，就是上次点击的城市
      localStorage.setItem("id",item.cityId)
      this.$router.go(-1)//点击时，后退一步
    }
  },
  computed:() {//将 state 的 list:[],放入到计算属性中
    ...mapState(["list"]),//获取state 的 list数据
    hotCity() {
      return this.list[0];
    },
    otherCity() {
      return this.list.slice(1);
    },
  },
};
</script>



# 二.将“详情页面”数据请求放在VueX中

1. 将数据接口，放在VueX中请求
<script>
import Vue from 'vue'
import Vuex from 'vuex'
import { getHotList } from "@/api";//引入'axios'请求

Vue.use(Vuex)

export default new Vuex.Store({
    state: {
      // 详情页面数据放在VueX中
      list:[],
    },
    mutations: {
      bbb(state,payload){//因为不可以直接获取 state中的 list:[]，需要在 mutations设置方法，并传值
        state.list = payload.data.data.not
      }
    },
    //详情页面异步函数
    actions: {//将异步的请求数据放在actions中
        async getData({commit}){ //异步转同步
            const res = await getHotList({id:this.id})//将传入的id = 马上使用的id
            commit("bbb",res)
        }
    }
})

2. 在组件中通过计算属性获取：Store仓库actions中的异步方法
<template>
    <div>
        <div v-if="list">//如果list存在，则显示 list的div
          <div>这是详情的页面--{{id}}</div>
          <p>{{list.nm}}</p>
          <!-- 此时不需要用v-for来遍历了，因为我们已经把id带进来了 -->
          <img :src="list.img | formatUrl" alt=""> //必须加 | formatUrl的方法，然后在<script>写
          <buttom @click="aaa">猜你喜欢</buttom>
        </div>
        <div v-else>loading...</div>//否则显示：loading...
    </div>
</template>

<script>
import { getHotList } from "@/api";//删除，因为直接在 Store仓库的 actions 中请求数据，所以不需要在组件中引入了

import { mapState,mapActions} from "vuex";

export default {
    props:["id"],//接收id

    mounted(){
      this.getData({id:this.id})
    },

    methods:{
      ...mapActions(["getData"]),
      aaa(){
        this.$router.push("@/详情")
      }
    },

    computed:{
      ...mapState(["list"])
    },

    filters:{ //图片不能直接显示，需要过滤器的方法
        formatUrl(val){
          return val && val.split("/w.h").join("/200.300")
                // 如果val存在，则才会有：val.split("/w.h").join("/200.300")
        }
    },
}








# 三.详情页面跳转到其他详情页面

1. 由于详情页面跳转到其他详情页面，虽然路由的路径改变了，但是页面还是没有改变

2. 原因是同样的组件系统会被复用

3. 解决办法一： this.$route 和 watch监听属性
 
             详情页到详情页，组件会进行服用（不会被销毁和重新创建了），系统为了提高性能

             用监听属性的:$route()方法----“猜你喜欢”时，才会使用
data(){
    return {
        id:""
    }
}
created() {
   this.id = this.$route.params.id
}
watch:{
   $route(val,oldval){
     <!-- console.log(val) -->新的
     <!-- console.log(oldval) -->旧的
     this.id = to.params.id  //取新的id
   } 
}


4. 解决办法二： 在自身组件中，使用：beforeRouteUpdata(to,from,next){}的方法
<script>
import { getHotList } from "@/api";//在"api"文件中引入对应的方法
export default {
    props:["id"],//接受id
    data(){
        return {
            list:{} //对象的类型
        }
    },
     async beforeRouteUpdata(to,from,next){
        const res = await getHotList({id:to.params.id})
        this.list = res.data.data.not
        next()
     }
}
</script>




# 四.将“最受欢迎的页面”数据请求放在VueX中

1. 将数据接口，放在VueX中请求
<script>
import Vue from 'vue'
import Vuex from 'vuex'
import { getHotList } from "@/api";

Vue.use(Vuex)

export default new Vuex.Store({
    state: {
      //最受欢迎的页面
      hotList: [],
    },
    mutations: {
      bbb(state,payload){//因为不可以直接获取 state中的 list:[]，需要在 mutations设置方法，并传值
        state.hotList = payload.data.data.not
      }
    },
    actions: {
      //最受欢迎的页面的异步函数
      getData({commit}){ 
        return new Promise((resolve)=>{
          getHotList().then((res))=>{
            commit("bbb",res)
            resolve()
          }
        })
      }
    }
  })

2. 在组件中通过计算属性获取：Store仓库actions中的异步方法
<template>
  <div class="HomeFavorable">
    <p class="hello">最受好评电影</p>
    <div class="wrapper">
      <ul>
        <li v-for="item in hotList" :key="item.id">
          <img :src="item.img" alt="" />
          <i>观众评分&nbsp;{{ item.mk }}</i>
          <span>{{ item.nm }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
let res
import { mapState,mapActions} from "vuex";}
import BetterScroll from "better-scroll";
export default {
  computed:{
    ...mapState(["hotList"])
  },
  mounted() {
    //这里不可以加 BetterScroll，必须是数据请求完毕以后才能添加,所以在actions内，加必须加 new Promis
    this.getData().then(()=>{
      this.$nextTick(() => {//这里不需要 this.$nextTick，因为有.then
        //在 mounted(){} 生命周期钩子内，加一个 this.$nextTick(()=>{}) 的方法，将 new BetterScroll缩写的实例对象放入里面
        new BetterScroll(".wrapper", {
          observeDOM: true,
          startX: 0,
          scrollX: true,
          scrollY: false,
          click: true,
        });
      });
    })
  },

###  也可以不用.then(),用 async 和await,但是在 Vuex 的 actions 中， return new Promise(()=>{}),还是要有的
  //  async mounted() {
  //   await this.getData()
  //       new BetterScroll(".wrapper", {
  //         observeDOM: true,
  //         startX: 0,
  //         scrollX: true,
  //         scrollY: false,
  //         click: true,
  //       });
  //   },
  methods: {
    ...mapActions(["getData"]),//方法中调用 actions的异步请求
  },
};
</script>

