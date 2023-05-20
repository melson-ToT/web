# 一.ui 组件库

1. Vant : 移动端 vue 组件库

2. 地址：https://youzan.github.io/vant-weapp/#/home

https://vant-ui.github.io/vant/#/zh-CN/swipe vue3

3. Element Ui ,地址：https://element.eleme.io/#/zh

4. youzan.githup.io

5. Vant适用vue的移动端

6. Element Ui适用于后台

7. Element Ui也可以用于PC，但是需要你用scss或者less重改  :scss或者less的重改，  需要scoped + /deep/ 方式（vue2）  ||  scoped + :deep 方式（vue3）




# 二.引入 ui 组件库

1. vue2 项目安装：npm i vant@latest-v2

2. vue3 项目安装：npm i vant

3. 在 main.ts 中引入：
                    import Vant from 'vant'
                    import 'vant/lib/index.css'

4. 在 main.ts 中: createApp(App).use(store).use(router).use(Vant).mount('#app')

5.  import 'vant/lib/index.css' 是将所有的 ui 组件库，全都引入进来

6. 命令行：npm i babel-plugin-import -D

7. 在src中建一个 .babel.config.js 的文件

8. 在main.js中
   删除：
   <!-- import "./assets/css.css"
   import "amfe-flexible" -->

   createApp(App).use(store).use(router)
   <!-- .use(Vant) -->
   .mount('#app')

   增加：
   用什么组件库，就引入
 import { Swipe, SwipeItem } from 'vant';

createApp(App)
.use(store)
.use(router)
.use(Vant)
<!-- .use(Swipe)
.use(SwipeItem) -->
.mount('#app')



8. 在组件中就不需要再引入了



# 三.组件中使用

1. https://vant-ui.github.io/vant/#/zh-CN vue3

2. 在组件中，直接复制 Vant的 HTML 和 CSS 代码,到组件中,

3. 按钮的案例
<template>
  <van-button type="primary">主要按钮</van-button>
</template>
<style lang="less">
#app {
    .van-button {
      width: 100%;
    }
}
</style>


# 四.头部开发

1. 在 Vant 中，找到 NavBar 导航栏

2. 在右边找到："标题"，选择相应"标题"的代码，粘贴带组件的 HTML 中
<template>
  <van-nav-bar title="首页" />
</template>

3. 左右有其他图标时
<template>
  <van-nav-bar title="标题" left-text="返回" left-arrow>
  <template #right>
    <van-icon name="search" size="18" />
  </template>
</van-nav-bar>
</template>

4. 如果左右图标不是自己想要的，只能通过具名插槽的方式

5. 样式变量
组件提供了下列 CSS 变量，可用于自定义样式，使用方法请参考 ConfigProvider 组件。

名称	默认值	描述
--van-nav-bar-height	46px





# 五.轮播图的案例

1. 复制过来
<template>
  <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
    <van-swipe-item>4</van-swipe-item>
  </van-swipe>
</template>

<style lang="less">
#app {
    .my-swipe .van-swipe-item {
    color: #fff;
    font-size: 20px;
    line-height: 150px;
    text-align: center;
    background-color: #39a9ed;
  }
}
</style>

2. 改写
<template>
  <van-nav-bar title="标题" />
  <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
                                                 <!-- 小球的颜色 -->
    <van-swipe-item v-for="item in list" :key="item">
      <img :src="item" alt="" />
    </van-swipe-item>
  </van-swipe>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
              //onMounted 是vue3 的 生命周期钩子
export default {
  setup() {
    const list = ref<string[]>([]);
	// list[]为:空
    onMounted(() => {
      fetch("http://www.pudge.wang:4000/home/banner")
        .then((response) => response.json())
        .then((res) => {
          //   console.log(res.result.list);
          list.value = res.result.list;
        });
    });
    return {
      list,
    };
  },
};
</script>

<style lang="less" scoped>
.my-swipe .van-swipe-item {
  height: 250px;

  img {
    width: 100%;
    height: 100%;
  }
}

/* /deep/ 是vue3 的写法，可以改写 Vant 的 css 样式 */
/* :deep()是vue2 的写法，可以改写 Vant 的 css 样式 */
/deep/.van-swipe__indicator {
  width: 30px;
  height: 8px;
  background: green;
  border-radius: 4px;
}
</style>



# 六.轮播图中嵌套搜索框
<template>
  <van-nav-bar title="标题" />
  <div class="ban">
    <van-search v-model="value" background="transparent" shape="round" placeholder="请输入搜索关键词" />
                                <!-- 搜索框添加透明度          边框为：圆形  -->
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="item in list" :key="item">
        <img :src="item" alt="" />
      </van-swipe-item>
    </van-swipe>
  </div>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
export default {
  setup() {
    const list = ref<string[]>([]);
    onMounted(() => {
      fetch("http://www.pudge.wang:4000/home/banner")
        .then((response) => response.json())
        .then((res) => {
          //   console.log(res.result.list);
          list.value = res.result.list;
        });
    });
    const value = ref<string>("")
    return {
      list,
      value,
    };
  },
};
</script>

<style lang="less" scoped>
.ban {
   position: relative; 
}

.van-search {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 10;
  width: 100%;
}

/* /deep/ 是vue3 的写法，可以改写 Vant 的 css 样式 */
/* :deep()是vue2 的写法，可以改写 Vant 的 css 样式 */
/* 将ui组件的内部样式进行修改 */
/deep/.van-field__control {
   background: rgba(255,255,255,0.1);

     /* 改变input框的字体颜色 */
    #van-search-1-input::placeholder {
    color: red;
  }
}


.my-swipe .van-swipe-item {
  height: 250px;

  img {
    width: 100%;
    height: 100%;
  }
}

/* /deep/ 是vue3 的写法，可以改写 Vant 的 css 样式 */
/* :deep()是vue2 的写法，可以改写 Vant 的 css 样式 */
/* 将ui组件的内部样式进行修改 */
/deep/.van-swipe__indicator {
  width: 30px;
  height: 8px;
  background: green;
  border-radius: 4px;
}

</style>



# 七.在 Vant 中，找到 Grid 宫格

1. 将对应的 HTML 代码 复制到对应的组件中

2. 改写文字

3. 将改写 icon="photo-o" 删除
<van-grid-item icon="photo-o" text="每日福利" />

4. 改写为双标签
<van-grid-item text="每日福利"></van-grid-item>

5. 在双标签内，使用具名插槽
<van-grid-item text="每日福利">
  <template #icon><img src="" alt=""></template>
</van-grid-item>

6. 案例
  <van-grid>
    <van-grid-item text="每日福利">
      <template #icon><img src="" alt=""></template>
    </van-grid-item>
    <van-grid-item text="每日福利">
      <template #icon><img src="" alt=""></template>
    </van-grid-item>
    <van-grid-item text="每日福利">
      <template #icon><img src="" alt=""></template>
    </van-grid-item>
    <van-grid-item text="每日福利">
      <template #icon><img src="" alt=""></template>
    </van-grid-item>
  </van-grid>

<style>
  .van-grid-item {
  img {
    width: 40px;
    height: 20px;
  }
}



# 八.在 Vant 中，找到 Grid 宫格，创建每行二个的图标

1. 在 Vant 中，找到 Grid 宫格 的自定义列数

2. 在一级标签内，加:column-num="3"
