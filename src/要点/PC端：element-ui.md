
# 一.vue2 项目创建：
1. git clone https://github.com/melson-ToT/vue-3.git

2. cd vue-2

3. 安装：npm i -g @vue/cli

4. vue create vue-2

5. 不要选择(vue3/vue2),选择 Manually select features

6. 选择：Babel、Router、Vuex、CSS Pre-processors、Linter / Formatter

7. 选择:2x

8. ? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) n(默认)选择哈希路由

9. > Sass/SCSS (with dart-sass) less,sass 都可以

# 10. > ESLint with error prevention only----不要报错
      ESLint + Airbnb config
      ESLint + Standard config
      ESLint + Prettier

# 11. >(*) Lint on save  ----这个
       ( ) Lint and fix on commit

# 12. > In dedicated config files  ----这个
        In package.json

13. ? Save this as a preset for future projects? (y/N) n

14. cd vue-2



# 二.element-ui 在PC端使用

1. 谷歌搜索 -> element-ui

2. 点击.Element - A Desktop UI Toolkit for Web

3. 安装：
      (1) vue2安装 ：npm i element-ui -S,

      (2) vue3 安装 ：npm i element-plus 

4. 在 main.js 中引入：()

      (1)：vue2
          import ElementUI from 'element-ui';
          import 'element-ui/lib/theme-chalk/index.css'//自带的样式
          Vue.use(ElementUI); 

      (2)：vue3
          import ElementPlus from 'element-plus';
          import 'element-plus/dist/index.css';
          .use(ElementPlus)



5. vue2：组件中需要的 ui 组件，在 element-ui 中，找到，然后将代码引入：
<template>
   <div>
      <el-button type="success">成功按钮</el-button>
   </div>
</template>




# 三.删除vue2自带的样式和组件

1. 将 src 中，自带的样式和组件删除

2. 在 assets 中，配置 css的重置样式表

3.  在 main.js 中引入：import './assets/css.css'



# 四.轮播图

1. https://element.eleme.io/#/zh-CN/component/carousel

2. 代码
<template>
  <div class="box">
    <el-carousel :interval="3000" type="card">
                  <!-- 图片自动切换时间：3秒 -->
      <el-carousel-item v-for="item in list" :key="item.id">
        <img :src="item.img" alt="" />
      </el-carousel-item>
    </el-carousel>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        {
          id: 1,
          img: "https://so2.360tres.com/sdm/420_627_/t01d7bcc974f60cdc86.webp",
        },
        {
          id: 2,
          img: "https://so2.360tres.com/sdm/417_417_/t01f23fc63a8a833188.webp",
        },
        {
          id: 3,
          img: "https://so2.360tres.com/sdm/365_259_/t0168ced599efb911bc.webp",
        },
        {
          id: 4,
          img: "https://so2.360tres.com/sdm/420_207_/t013808ea0e0454bb7b.webp",
        },
      ],
    };
  },
};
</script>

<style lang="less">
.box {
  width: 100%;
  height: 100%;
  .el-carousel {
   /* 相当于ul标签 */
    width: 800px;
    height: 400px;
    margin: 50px auto;
    overflow: hidden;
    .el-carousel-item {
      /* 相当于li标签 */
      img {
        width: 800px;
        height: 400px;
      }
    }
    .el-carousel__button {
       /* 下面的指示器 */
      background: red;
    }
  }
}
</style>
