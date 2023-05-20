# 一.vue3 中是没有 tag 的改写标签

1. vue3 中是没有 tag 的改写标签

2. 可以在 <router-link class="li">后面加一个 class名

<template>
  <div class="footer">
    <router-link class="li" v-for="(item, index) in list" :key="index"
     :to="'/home' + item.router">
     <!-- tag="li" -->
      <span :class="'iconfont icon-' + item.icon"></span>
      <span>{{ item.title }}</span>
    </router-link>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
export default {
  setup() {
    const list = ref([
      {
        title: "首页",
        icon: "shouye",
        router:"/page",
      },
      {
        title: "分类",
        icon: "fenlei",
        router: "/ification",
      },
      {
        title: "购物车",
        icon: "gouwuchekong",
        router:"/Shopping",
      },
      {
        title: "我的",
        icon: "wode",
        router:"/my",
      },
    ]);
    return {
      list,
    };
  },
};
</script>

<style lang="less" scoped>
.footer {
  background: #fff;
  width: 100%;
  height: 48px;
  border-top:1px solid black;
  display: flex;
  justify-content: space-around;
  position: fixed;
  left: 0;
  bottom: 0;
  align-items: center;

  &>.li {
    height: 100%;
    width: calc(100% / 4);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;

    .iconfont {
      font-size: 20px;
    }

    span:last-child {
      font-size: 12px;
    }
  }
  .router-link-active {
    color: red;
  }
}
</style>