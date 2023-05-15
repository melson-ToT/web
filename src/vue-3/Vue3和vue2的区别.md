# 一.区别1

1. vue2: new vue({})

2. vue3:  vue.createAPP(根组件).mount(组件class名)

3. vue3的<template>内可以允许多个根元素

4. 生命周期：销毁前钩子
          将之前的：beforeDestroy(){}
          改为：beforeUnmount(){}


# 二.区别2

1. 点击按钮，给input进行数据绑定

2. 谁用，就给谁绑定

3. 将input输入的内容，添加给ul.

4. 再将input输入框内容清空

5. list[] =  list[].过滤(原来的id不等于现在的id)  ----一旦不等于，就会删除

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


# 三.区别3

1. 事件修饰符不能使用按键码 --13

2. 依赖注入有响应式了

3. 过滤器被删除了--(在标签中就不需要过滤器了)，但是在方法中还是要写入的
<!-- this.list = this.list.filter(item=>item.id != id) -->


# 四.显示实时变动的时间
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
    setInterval(()=>{//每秒钟加1秒
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
};
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>




# 五.组合API

1. setup()他是组合api的入口，同时也是生命周期

2. setup()是在 bedoreCreate(){} 之前创建的，并且没有 this

3. 案例：
<template>
  <span>{{count}}</span>
  <button @click="fn">按钮</button>
</template>

<script>
//如果需要有响应式，需要 ref 的方法
import { ref } from "vue"

export default {
  setup() {
    let count = ref(10)//ref：创建一个引用
    const fn = () => {
      // console.log(count.value); 打印 count 的10 在哪里
      count.value++
    }
    //必须要有 return ，只有 return 的内容才可以在 <template> 里面使用
    return {
      count,
      fn
    };
  },
};
</script>

4. 所有的变量、方法、计算属性，都写在 setup(){}生命周期内：

                (1).先用：let 或 const
                (2).引入 ref 的方法
                (3).将定义的变量写在 return{} 内



