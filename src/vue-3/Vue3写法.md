
vue3 的写法：
          1. 数据变量：
                     需要引入 ：import { ref } from "vue";
                     定义：const count = ref(3)
                     注册：return：{
                                    count 
                                  }
                     外部提取：count.value

          2. 方法：
                    定义： const fn = () => {
                            count.value ++
                          }
                    注册：return：{
                                   fn 
                                 }

          3. 生命周期：
                    需要引入 ：import { onMounted, onUpdated, onBeforeUnmount} from "vue"
                    使用： onMounted(() => {//挂载
                            console.log("onMounted1");
                          }),

          4. 监听属性：
                    需要引入 ：import { watch } from "vue";
                    使用： watch(count,(val,oldal) => {//watch监听
                            console.log(count,val,oldal);
                          })

          5. 计算属性：
                    需要引入 ：import { computed } from "vue";
                    使用：const doubleCount = computed(() => {
                            return count.value * 2
                         })
                    注册：return：{
                                   doubleCount 
                                 }






# 一.vue2 的写法：
               添加列表
<template>
   <input type="text" v-model="value">
   <button @click="fn">添加</button>
   <ul>
    <li v-for="item in list" :key="item.id">{{item.name}} - <button @click="fa(item.id)">删除</button></li>
   </ul>
</template>

<script>
export default {
  data(){
    return {
      value:"",
      list:[
        {
          name:"zhangsan",
          id:1
        },
        {
          name:"lisi",
          id:2
        }
      ]
    }
  },
  methods:{
    fn(){
      this.list.push({//
        id:new Date().getTime(),
        name:this.value
      }),
      this.value=""
    },
    fa(id){
      this.list = this.list.filter(item=>item.id != id)
      // list[] =  list[].过滤(原来的id不等于现在的id)  ----一旦不等于，就会删除
    }
  }
}
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

</style>




# 二.vue3 的写法：
               添加列表
<template>
   <input type="text" v-model="value">
   <button @click="fn">添加</button>
   <ul>
    <li v-for="item in list" :key="item.id">{{item.name}} - <button @click="fa(item.id)">删除</button></li>
   </ul>
</template>

<script>
import { ref } from "vue";
export default {
  data(){

    const value = ref("")

    const list = ref([
        {
          name:"zhangsan",
          id:1
        },
        {
          name:"lisi",
          id:2
        }
      ])

    const fn = ()=> {
        this.list.push({
        id:new Date().getTime(),
        name:this.value
      }),
      this.value=""
    }

    const fa = (id) => {
      this.list = this.list.filter(item=>item.id != id)
    }

    return {
      value,
      list,
      fn,
      fa,
    }
  },
}
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

</style>




# 三.vue2 的写法：
               显示实时变动的时间
<template>
  <p>{{ fathTime }} - <button @click="fb">暂停</button></p>
  <!-- 时间戳转日期 -->
  <input type="text" v-model="value" />
  <button @click="fn">添加</button>
  <ul>
    <li v-for="item in list" :key="item.id">
      {{ item.name }} - <button @click="fa(item.id)">删除</button>
    </li>
  </ul>
</template>

<script>
let dsq
export default {
  data() {
    return {
      value: "",
      list: [
        {
          name: "zhangsan",
          id: 1,
        },
        {
          name: "lisi",
          id: 2,
        },
      ],
      timer: 0,
    };
  },

  mounted() {
    dsq = setInterval(()=>{//每秒钟加1秒
      this.timer = new Date().getTime();
    },1000)
  },

  computed: {
    fathTime() {
      // 网上搜时间戳转日期
        let date = new Date(this.timer);
        let year = date.getFullYear();
        let month= date.getMonth() + 1;
        month= month< 10 ? ('0' + month) : month;
        let day = date.getDate();
        day = day < 10 ? ('0' + day ) : day ;
        let h = date.getHours();
        h = h < 10 ? ('0' + h) : h;
        let m = date.getMinutes();
        m = m < 10 ? ('0' + m) : m;
        let s = date.getSeconds();
        s = s < 10 ? ('0' + s) : s;
        return year + '-' + month + '-' + day + ' ' + h + ':' + m + ':' + s;
    },
  },

  methods: {
    fn() {
      this.list.push({
        id: new Date().getTime(),
        name: this.value,
      }),
        (this.value = "");
    },
    fa(id) {
      this.list = this.list.filter((item) => item.id != id);
    },
    fb(){//暂停时间
      clearInterval(dsq)
    }
  },
  beforeUnmount(){
    clearInterval(dsq)
  }
};
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>           



# 四.vue3 的写法：
               显示实时变动的时间

<template>
  <p>{{ fathTime }} - <button @click="fb">暂停</button></p>
  <!-- 时间戳转日期 -->
  <input type="text" v-model="value" />
  <button @click="fn">添加</button>
  <ul>
    <li v-for="item in list" :key="item.id">
      {{ item.name }} - <button @click="fa(item.id)">删除</button>
    </li>
  </ul>
</template>

<script>
let dsq;
import { ref } from "vue";
export default {
  data() {
    const value = ref("");

    let timer = 0;

    const list = ref([
      {
        name: "zhangsan",
        id: 1,
      },
      {
        name: "lisi",
        id: 2,
      },
    ]);

    const dsq = () => {
      setInterval(() => {
        this.timer = new Date().getTime();
      }, 1000);
    };

    const fathTime = () => {//计算属性，这里的写法是错误的
      // 网上搜时间戳转日期
      let date = new Date(this.timer);
      let year = date.getFullYear();
      let month = date.getMonth() + 1;
      month = month < 10 ? "0" + month : month;
      let day = date.getDate();
      day = day < 10 ? "0" + day : day;
      let h = date.getHours();
      h = h < 10 ? "0" + h : h;
      let m = date.getMinutes();
      m = m < 10 ? "0" + m : m;
      let s = date.getSeconds();
      s = s < 10 ? "0" + s : s;
      return year + "-" + month + "-" + day + " " + h + ":" + m + ":" + s;
    };

    const fn = () => {
      this.list.push({
        id: new Date().getTime(),
        name: this.value,
      }),
        (this.value = "");
    };

    const fa = (id) => {
      this.list = this.list.filter((item) => item.id != id);
    };

    const fb = () => {
      clearInterval(dsq);
    };

    return {
      value,
      timer,
      list,
      dsq,
      fathTime,
      fn,
      fa,
      fb,
    };
  },

  beforeUnmount() {
    clearInterval(dsq);
  },
};
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
