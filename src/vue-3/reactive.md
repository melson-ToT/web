# 一.正常写法：
<template>
  <p>{{name}}</p>
  <p>{{age}}</p>
  <p>{{dizhi}}</p>
  <button @click="fn">点击</button>
</template>
  
<script>

import { ref } from "vue";

export default {
  setup() {
    const name = ref("zhansan")

    const age = ref(20)

    const dizhi  = ref("安徽")

    const fn = () => {
      console.log(111);
      age.value = 30
    }

    return {
      name,
      age,
      dizhi,
      fn,
    }
  },

};
</script>


# 二.利用 reactive的方式进行简写：

<template>
  <p>{{data.name}}</p>
  <p>{{data.age}}</p>
  <p>{{data.dizhi}}</p>
<!-- 在使用的时候就data.name 来拿到数据 -->
  <button @click="fn">点击</button>
</template>
  
<script>

// import { ref } from "vue";----不是要ref，所以要删除

import { reactive } from "vue";

export default {
  setup() {

    const data = reactive({//以对象的形式，将数据放在 reactive 内
      name:"zhansan",
      age:20,
      dizhi:"安徽",
    })

    // const name = ref("zhansan")

    // const age = ref(20)

    // const dizhi  = ref("安徽")

    const fn = () => {
      console.log(111);
      data.age.value = 30
    }

    return {
      // name,
      // age,
      // dizhi,
      fn,
      data,
    }
  },
};
</script>