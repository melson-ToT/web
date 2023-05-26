
# 一.侧边栏 ---相同的内容
<template>
  <div class="bott-sj">
    <ul>
      <li
        v-for="(item, index) in shujulist"
        :key="item.id"
        @click="active = index"
        :style="{ background: active === index ? '#eee' : '' }"
      >
        <span :style="{ color: active === index ? 'red' : '' }">{{
          item.span
        }}</span>
      </li>
    </ul>
    <div class="box"></div>
    <!-- 如果页面相同，则采用一样的页面 -->
  </div>
</template>

<script>

export default {
  data() {
    return {
      shujulist: [
        {
          id: 1,
          span: "张非",
        },
        {
          id: 2,
          span: "小康",
        },
        {
          id: 3,
          span: "张浩",
        },
        {
          id: 4,
          span: "义军",
        },
      ],

      active: 0,
    };
  },

};
</script>

<style lang="less" scoped>
.bott-sj {
  width: 100%;
  height: calc(100% - 150px);
  display: flex;
  ul {
    width: 300px;
    height: 100%;
    background: #afafaf;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    li {
      width: 100%;
      height: calc(100% / 4);
      display: flex;
      justify-content: center;
      align-items: center;
      span {
        font-size: 25px;
        color: #000;
      }
    }
  }
}
</style>




# 二.侧边栏 ---不同的内容
<template>
  <div class="bott-sj">
    <ul>
      <li
        v-for="(item, index) in shujulist"
        :key="item.id"
        @click="active = index"
        :style="{ background: active === index ? '#eee' : '' }"
      >
        <span :style="{ color: active === index ? 'red' : '' }">{{
          item.span
        }}</span>
      </li>
    </ul>
    <AaaA v-if="active === 0"/>
    <BbbB v-if="active === 1"/>
    <CccC v-if="active === 2"/>
    <DddD v-if="active === 3"/>
      <!-- 如果页面不同，则采用子组件切换 -->
  </div>
</template>

<script>
import AaaA from "./ABCD/AaaA.vue";
import BbbB from "./ABCD/BbbB.vue";
import CccC from "./ABCD/CccC.vue";
import DddD from "./ABCD/DddD.vue";
export default {
  data() {
    return {
      shujulist: [
        {
          id: 1,
          span: "张非",
        },
        {
          id: 2,
          span: "小康",
        },
        {
          id: 3,
          span: "张浩",
        },
        {
          id: 4,
          span: "义军",
        },
      ],

      active: 0,
    };
  },
  components: {
    AaaA,
    BbbB,
    CccC,
    DddD,
  },
};
</script>

<style lang="less" scoped>
.bott-sj {
  width: 100%;
  height: calc(100% - 150px);
  display: flex;
  ul {
    width: 300px;
    height: 100%;
    background: #afafaf;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    li {
      width: 100%;
      height: calc(100% / 4);
      display: flex;
      justify-content: center;
      align-items: center;
      span {
        font-size: 25px;
        color: #000;
      }
    }
  }
}
</style>
