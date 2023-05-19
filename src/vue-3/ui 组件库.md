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


4. 轮播图的案例
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




