
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
          Vue.use(ElementUI); 

      (2)：vue3
          import ElementPlus from 'element-plus';
          import 'element-plus/dist/index.css';
          .use(ElementPlus)



5. 组件中需要的 ui 组件，在 element-ui 中，找到，然后将代码引入：
<template>
   <div>
      <el-button type="success">成功按钮</el-button>
   </div>
</template>




# 三.删除vue2自带的样式和组件

1. 将 src 中，自带的样式和组件删除

2. 在 assets 中，配置 css的重置样式表

3.  在 main.js 中引入：import './assets/css.css'



# 四

