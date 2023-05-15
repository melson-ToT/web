
# 一.生命周期钩子

1. 在 setup 内，自带 bedoreCreate(){}和created(){} 钩子

2. 如果想写创建阶段的代码，直接写在 setup 内

3. 生命周期全部加上 on ,首字母大写，要在 vue 内解构，并且里面传入回调函数

4. 案例：

<template>
  <p>生命周期</p>
</template>

<script>
import { onMounted, onUpdated, onBeforeUnmount} from "vue"//引入生命周期钩子

export default {
  setup() {
    
    onMounted(() => {//挂载
      console.log("onMounted");
    }),

    onUpdated(() => {//更新
      console.log("onUpdated");
    }),

    onBeforeUnmount(() => {//销毁
      console.log("onBeforeUnmount");
    })

    return {
    };
  },
};
</script>

5. 组件中多个功能方法，可以将不同的功能，写入一样的生命周期，实现功能分离，
<script>
import { onMounted, onUpdated, onBeforeUnmount} from "vue"//引入生命周期钩子

export default {
  setup() {
    
    onMounted(() => {//挂载
      console.log("onMounted1");
    }),

    onMounted(() => {//挂载
      console.log("onMounted2");
    }),

    onMounted(() => {//挂载
      console.log("onMounted3");
    }),

    return {
    };
  },
};
</script>