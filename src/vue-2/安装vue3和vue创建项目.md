# 一.vue3 项目创建：
1. git clone https://github.com/melson-ToT/vue-3.git

2. cd vue-3

3. 安装：npm i -g @vue/cli

4. vue create vue-3

5. 不要选择(vue3/vue2),选择 Manually select features

6. 选择：Babel、Router、Vuex、CSS Pre-processors、Linter / Formatter

7. 选择:3x

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



# 二.vue2 项目创建：
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



# 二.项目结构
1. node_modules  项目依赖
2. public 静态资源目录
3. favicon.ico  页面小图标
4. index.html  页面唯一的html文件，不会去修改他（单页面应用 SPA）
5. 文件中package.json中的"script"有"serve"是启动项目的
6. 启动项目：npm run serve 回车键
7. src 开发目录
8. jsconfig.json 记录装载了那些文件
9. vue.config.js 我们需要操作的项目配置文件


# 三.需要安装的插件
1. vetur
2. prettier


# 四.src目录：
1. main.js  项目入口文件(当启动文件时，最先启动的文件)
2. App.vue  项目的根组件
3. saaete   项目的静态文件(放静态的css/js/imge/font文件)
4. components 放组件的文件夹
5. router   项目的路由文件夹
6. store  项目的vuex的仓库文件夹
7. views  页面的组件


# 五. 严格模式对代码的影响和解决办法
1. 找到package.json，在命令行，删除相应vue全家桶代码的严格模式：npm unstyle 对应的文件

2. 严格模式，注释这两行
  extends: [
    "plugin:vue/essential",
    // "eslint:recommended",
    // "plugin:prettier/recommended",
  ],



