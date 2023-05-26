
# 一.侧边栏 ---组件库
<template>
  <div class="father">
    <div class="fenlei">分类</div>
    <div class="buttom">
      <van-sidebar v-model="active">
        <van-sidebar-item v-for="(item, index) in list" :key="index" :title="item.title"/>
      </van-sidebar>
      <div class="box">{{ log[active].res }}</div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { Sidebar, SidebarItem } from "vant";

export default {
  setup() {
    const list = ref([
      {
        title: 1,
      },
      {
        title: 2,
      },
      {
        title: 3,
      },
    ]);


    const log = ref([
      {
        res: "44444",
      },
      {
        res: "55555",
      },
      {
        res: "66666",
      },
    ]);

    const active = ref(0);

    return {
      active,
      list,
      log,
    };
  },
};
</script>

<style lang="less" scoped>
.father {
  width: 100%;
  height: 100%;
  .fenlei {
    width: 100%;
    height: 50px;
    background: pink;
    text-align: center;
    line-height: 50px;
  }
  .buttom {
    width: 100%;
    height: calc(100% - 50px);
    display: flex;
    .van-sidebar {
      width: 60px;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      .van-sidebar-item {
        display: flex;
        flex: 1;
        &::before {
          width: 6px;
          height: 100%;
          background: red;
        }
      }
    }
    
  }
}
</style>



# 二.侧边栏 ---原生

1. 简单类型
<li v-for="(item, index) in list" :key="index" @click="active=index" :style="{color:active === index?'red':''}">

2. 复杂类型
<li v-for="(item, index) in list" :key="index" @click="activeindex=index" :class="{ active: activeindex === index }">

<template>
  <div class="father">
    <div class="fenlei">购物车</div>
    <div class="buttom">
      <ul>
        <li v-for="(item, index) in list" :key="index" @click="activeindex=index" :class="{ active: activeindex === index }">
          <span>{{item.title}}</span>
        </li>
      </ul>
      <div class="box">{{ log[activeindex].res }}</div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const list = ref([
      {
        title: "帽子",
      },
      {
        title: "衣服",
      },
      {
        title: "鞋子",
      },
    ]);
    const log = ref([
      {
        res: "44444",
      },
      {
        res: "55555",
      },
      {
        res: "66666",
      },
    ]);
    // const fn = ((index)=>{
    //   active.value = index
    // })
    const activeindex = ref(0);

    return {
      activeindex,
      list,
      log,
    };
  },
};
</script>

<style lang="less" scoped>
.father {
  width: 100%;
  height:calc(100% - 49px);
  .fenlei {
    width: 100%;
    height: 50px;
    background: pink;
    text-align: center;
    line-height: 50px;
  }
  .buttom {
    width: 100%;
    height: calc(100% - 50px);
    display: flex;
    ul {
      width: 60px;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      background: burlywood;
      li {
        width: 100%;
        height: calc(100% / 3);
        border-bottom: 1px solid black;
        box-sizing: border-box;
        background: burlywood;
        color: #fff;
        font-size: 22px;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
      }
      .active {
        background: blueviolet;
        &::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 8px;
            height: 100%;
            background: red;
        }
      }
    }
    
  }
}
</style>



# 三.组件的二层嵌套
<template>
  <div class="bott-sj">
    <ul>
      <li
        v-for="(item, index) in shujulist"
        :key="item.id"
        @click="active = index"
        :style="{ background: active === index ? '#eee' : '' }"
      >
        <span :style="{ color: active === index ? 'red' : '' }" >{{
          item.span
        }}</span>
      </li>
    </ul>
    <AaaA v-if="active === 0"/>
    <BbbB v-if="active === 1"/>
    <CccC v-if="active === 2"/>
    <DddD v-if="active === 3"/>
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
  background:#eee;
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