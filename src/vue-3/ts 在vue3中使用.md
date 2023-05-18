# 一.安装和使用ts 

1. git clone https://github.com/melson-ToT/vue-3.git

2. cd vue-3

3. npm config set registry https://registry.npm.taobao.org(国内源)

4. 安装：vue create ts-cli

5. 不要选择(vue3/vue2),选择 Manually select features

6. 选择：Babel、TypeScript、Router、Vuex、CSS Pre-processors、Linter / Formatter

7. 选择:3x

8. ? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) n(默认)选择哈希路由

9. ? Use Babel alongside TypeScript (required for modern mode, auto-detected polyfills, transpiling JSX)? (Y/n) n

10. > ESLint with error prevention only  这个
      ESLint + Airbnb config
      ESLint + Standard config
      ESLint + Prettier

11. n

12. cd ts-cli

13. 启动项目 npm run serve



# 二.ts-cli 的项目删写

1. 在App.vue中删除
<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
</template>

<script lang="ts">
import { defineComponent } from 'vue';
// import HelloWorld from './components/HelloWorld.vue';

export default defineComponent({
//   name: 'App',
//   components: {
//     HelloWorld
//   }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

2. 删除 components文件的内容

3. 删除 assets 文件



# 三.ts-cli 的项目，点击事件 ++ 或 --

1. ++ 或 --
<template>
  <h2>vue3 + ts</h2>
  <button @click="fa">-</button>
  <span>{{ count }}</span>
  <button @click="fb">+</button>
</template>

<script lang="ts">
import { defineComponent,ref } from 'vue';

export default defineComponent({
  setup(){
    const count = ref<number>(5);

    const fa = ():void => {
      count.value--
    }

    const fb = ():void => {
      count.value++
    }

    return {
      count,
      fa,
      fb,
    }
  }
});
</script>

2. 如果是要 +2 或 -2,  :void表示:没有返回值  ，num1:number：形参，类型：数字
<template>
  <h2>vue3 + ts</h2>
  <button @click="fa(2)">-</button>
  <span>{{ count }}</span>
  <button @click="fb(2)">+</button>
</template>

<script lang="ts">
import { defineComponent,ref } from 'vue';

export default defineComponent({
  setup(){
    const count = ref<number>(5);

    const fa = (num1:number):void => {
      count.value -= num1
      if(count.value <= 0){//如果小于0，则等于0
        count.value = 0
      }
    }

    const fb = (num2:number):void=> {
      count.value += num2
    }

    return {
      count,
      fa,
      fb,
    }
  }

});
</script>



# 四.ts-cli 的项目，watch 监听
<template>
  <h2>vue3 + ts</h2>
  <button @click="fa(2)">-</button>
  <span>{{ count }}</span>
  <button @click="fb(2)">+</button>
</template>

<script lang="ts">
import { defineComponent,ref,watch } from 'vue';

export default defineComponent({
  setup(){
    const count = ref<number>(5);

    const fa = (num1:number):void => {
      count.value -= num1
      if(count.value <= 0){
        count.value = 0
      }
    }

    const fb = (num2:number):void=> {
      count.value += num2
    }

    watch(count,(val) =>{//监听 count新数据的变化值
      console.log(val);
      
    })

    return {
      count,
      fa,
      fb,
    }
  }

});
</script>


# 五.ts-cli 的项目，计算属性

1. 计算属性，是基于 count ，来重新得到一个值，dou

2. 当 count 改变时，dou内也有count，所以也跟着改变

<template>
  <button @click="fa(2)">-</button>
  <span>{{ count }}</span>--<span>{{ dou }}</span>
  <button @click="fb(2)">+</button>
</template>

<script lang="ts">
import { computed, defineComponent,ref,watch } from 'vue';

export default defineComponent({
  setup(){
    const count = ref<number>(5);

    const fa = (num1:number):void => {
      count.value -= num1
      if(count.value <= 0){
        count.value = 0
      }
    }

    const fb = (num2:number):void=> {
      count.value += num2
    }

    watch(count,(val) =>{
      console.log(val);
      
    })

    const dou = computed<number>(() =>{
      return count.value * 2
    })

    return {
      count,
      fa,
      fb,
      dou,
    }
  }

});
</script>



# 六.input框的双向数据绑定
<template>
  <input type="text" v-model="value">
  <button @click="fn">添加</button>
  <ul>
    <li v-for="item in list" :key="item.id">{{item.name}}--<button @click="fa(item.id)">删除</button></li>
  </ul>
</template>

<script lang="ts">
import { defineComponent,ref } from 'vue';

interface ChildType {
  id:number,
  name:string,
}

export default defineComponent({
  setup(){
    const list = ref<ChildType[]>([
      {
        id:1,
        name:"zhangsan",
      },
      {
        id:2,
        name:"lisi",
      },
    ])

    const value = ref<string>("")

    const fn = ():void =>{
      list.value.push({
        id:new Date().getDate(),
        name:value.value
      })
    }

    const fa = (id:number) => {
      list.value = list.value.filter(item =>item.id != id)
    }

    return {
      list,
      value,
      fn,
      fa,
    }
  }

});
</script>


