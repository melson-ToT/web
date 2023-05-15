# 一.使用setup函数时，接受两个参数

1. props：就是 父传子

2. context：就是 子传父  -- context.enit("")

3.  setup(props,context) {},



# 二.使用setup函数时，setup可以接收第一个参数是props

1. 父组件 --（父传子）
<template>
  <ZhangFei name="zhangsan"/>
</template>
  
<script>
import ZhangFei from "./ZhangFei.vue";
export default {
  setup() {},
  //注册组件只能写在setup的外面
  components: {
    ZhangFei,
  },
};
</script>


2. 子组件，通过 props:[]来接收
<template>
  <p>我是子组件--{{ name }}--{{ name2 }}</p>
</template>

<script>
import { ref } from "vue";
export default {
  //porps接收数据也要写在setup外面
  props: ["name"],

  setup(props) {
    //setup可以接收第一个参数是props，内部的数据就可以来获取props的值
    const name2 = ref(props.name);

    return {
      name2,
    };
  },
};
</script>

<style lang="less" scoped>
</style>



# 三.使用setup函数时，setup可以接收第二个参数是context

1. （子传父）
2.  this.$emit = context.emit

3. 父组件
<template>
  <ZhangFei name="zhangsan" @getName="getName"/>
</template>
  
<script>
import ZhangFei from "./ZhangFei.vue";
export default {
  setup() {
    const getName = ()=> {
      console.log("getName");
    }

    return {
      getName,
    }
  },
  //注册组件只能写在setup的外面
  components: {
    ZhangFei,
  },
};
</script>

4. 子组件
<template>
  <p>我是子组件--{{ name }}--{{ name2 }}</p>
</template>

<script>
import { ref ,onMounted } from "vue";
export default {
  //porps接收数据也要写在setup外面
  props: ["name"],

  setup(props,context) {
    //setup可以接收第一个参数是props，内部的数据就可以来获取props的值
    const name2 = ref(props.name);

    onMounted(() => {
      //this.$emit = context.emit
      context.emit("getName")
    })

    return {
      name2,
    };
  },
};
</script>

<style lang="less" scoped>
</style>