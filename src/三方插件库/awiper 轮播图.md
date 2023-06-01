# 一.awiper 轮播图

1. 安装 npm i swiper@5  vue2    7、8用于vue3

2. 在组件中引入 swiper
import Swiper from 'swiper'
import 'swiper/css/swiper.min.css'

3. https://www.bilibili.com/video/BV1TY4y1z7Z8/?spm_id_from=333.337.search-card.all.click




# 二.awiper 轮播图 在组件中使用

1. HTML
<div class="swiper">
    <div v-if="banner.length" class="swiper-container">
    <!-- swiper-wrapper 是vue3的版本，swiper-container 是vue2的版本-->
        <div v-for="iten in banner" :key="item.id" class="swiper-slide">
          <img :src="item.img" />
        </div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
    <!-- 删除滚动条
    <div class="swiper-scrollbar"></div> -->
</div>

2. CSS
.swiper-container {
    width: 600px;
    height: 30px;
}  

3. JS
<script>  
import Swiper from 'swiper'
import 'swiper/css/swiper.min.css'  
import axios from 'axios'
export default { 
  data(){
    return {
      banner:[]
    }
  },
  async created(){
    const res = await axios.get("http://localhost:8888/banner"){
    this.banner = res.data.img
    }
  },
  updated() {//更新后才能使用，这里不能使用 挂载钩子
    new Swiper ('.swiper-container', {
    // direction: 'vertical',  删除垂直切换选项
    loop: true, // 循环模式选项
    
    // 如果需要分页器
    pagination: {
      el: '.swiper-pagination',
    },
    
    // 如果需要前进后退按钮
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
    
    // 删除滚动条
    scrollbar: {
      el: '.swiper-scrollbar',
    },
    effect: 'fade',
  }) 
  }
 
}       
  </script>



# awiper 轮播图 的api文档的

1. 图片的渐变
在 Effects(切换效果)。点击 effect ，在代码中复制：effect: 'fade',粘贴到 updated()钩子的最后的配置中

