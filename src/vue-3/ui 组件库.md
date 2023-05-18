# 一.ui 组件库

1. Vant : 移动端 vue 组件库

2. 地址：https://youzan.github.io/vant-weapp/#/home

3. Element Ui ,地址：https://element.eleme.io/#/zh

4. youzan.githup.io



# 二.引入 ui 组件库

1. vue2 项目安装：npm i vant@latest-v2

2. vue3 项目安装：npm i vant

3. 在 main.ts 中引入：
                    import Vant from 'vant'
                    import 'vant/lib/index.css'

4. 在 main.ts 中: createApp(App).use(store).use(router).use(Vant).mount('#app')



# 三.组件中使用

1. 在组件中，直接使用 Vant 组件库的 代码
<van-button type="primary">主要按钮</van-button>




