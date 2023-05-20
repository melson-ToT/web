# 一.下载图标
1. 打开阿里图标，搜索相应的图标
2. 将相应的图标加入购物车
3. 点击购物车，点击：下载代码
4. 点击左下角的.zip
5. 在项目的src种创建一个文件中assets文件夹
6. 点击下载的文件中，点击：解压到对应的项目的assets文件夹中


# 二.引入图标
1. 引入项目下面生成的fontclass的代码：
                                  1.在main.js中引入文件
                                  2.import "./assets/font_k1hyk6b1km/iconfont.css"
                                  3.在下载的图标中，D盘，项目，src文件的图标中查看，点击 Font class，复制相应的.icon-名，不要.

2. 挑选相应的图标，并获取类名，应用于页面
                                  1.在对应的项目<template>中，建立标签，取class名，在""内，写 iconfont icon-名
                                   <span class="iconfont icon-caidan"></span>

<template>
  <header>
    猫眼电影
    <span class="iconfont icon-caidan"></span>
  </header>
</template>

<script>
export default {
  name: "HomeIndex",
};
</script>

<style lang="less" scoped>
header {
  width: 100%;
  height: 50px;
  background: #e54847;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18px;
  color: #fff;
  position: relative;

  .iconfont {
    position: absolute;
    top: calc(100% - 24px) / 2;
    right: 15px;
    font-size: 24px;
  }
}
</style>


# 底部：foore
<script>
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const routes = [
    {
        path: "/", 
        redirect:"/home",//默认为重定向
    },
    {
        path: "/home", 
        component: () => import("../views/Home/HomeF.vue"),
        children:[
            {
                path: "/home", 
                redirect: "/home/film",
            },
            {
                path: "/home/film", 
                component: () => import("../views/Home/HomeN/HomeIndex.vue"),
                meta:{requireAlive:true}//页面切换时，保持原来的操作，不会被销毁
            },
            {
                path: "/home/video", 
                component: () => import("../views/Home/HomeN/HomeMy.vue"),
                meta:{requireAlive:false}//页面切换时，被销毁
            },
            {
                path: "/home/Smallvideo", 
                component: () => import("../views/Home/HomeN/HomeSmallvideo.vue"),
                meta:{requireAlive:false}
            },
            {
                path: "/home/broadcast", 
                component: () => import("../views/Home/HomeN/HomeBroadcast.vue"),
                meta:{requireAlive:false}
            },
            {
                path: "/home/my", 
                component: () => import("../views/Home/HomeN/HomeMy.vue"),
                meta:{ requireLogin:true, requireAlive:false},
            },
        ]
    },

    {
        path: "/login", 
        component: () => import("../views/LogIn/LogIn.vue"),
    },
    {
        path: "/city", 
        component: () => import("../views/city/cityIndex.vue")  
    },
    {
        path: "/detail/:id", 
        props:true,
        component: () => import("../views/detail/detailIndex.vue")  
    },
    {
        path: "*", //404报错
        component:() => import("../views/NotFound/NotFound.vue")
    }
]

const router = new VueRouter({
    routes,
})

//全局路由守卫
//只要路由发生改变，就会执行
// router.beforeEach((to,from,next)=>{
//     //console.log(to);
//     //console.log(from);
//     if(to.path === "/home/my"){//判断（去到的哈希值，如果等于 对应的哈希值页面）
//         if(localStorage.getItem("token")){ //判断（如果有("token"）
//             next()//守卫放行
//         }else{
//             next("/login")//否则去登录页
//         }
//     }else{//其他的放行
//         next()//守卫放行
//     }
// })

//全局路由守卫配合元信息的方法
router.beforeEach((to,from,next)=>{
    //console.log(to);
    //console.log(from);
    if(to.meta.requireLogin){//判断（如果去对应的哈希值页面，）
        if(localStorage.getItem("token")){ //判断（如果有("token"）
            next()//守卫放行
        }else{
            next("/login")//否则去登录页
        }
    }else{//其他的放行
        next()//守卫放行
    }
})


const originalPush = VueRouter.prototype.push
VueRouter.prototype.push = function push(location) {
  return originalPush.call(this, location).catch((err) => err)
}


export default router

<template>
  <div class="HomeFooter">
    <router-link v-for="(item, index) in tabList" :key="index" 
      :to="'/home'+item.router"
      tag="div">
      <span :class="'iconfont icon-' + item.icon"></span>
      <span>{{item.title}}</span>
    </router-link>
  </div>
</template>

<script>
export default {


  data() {
    return {
        tabList: [
          {
            title: '电影',
            icon: 'dianying',
            router:"/film"
          },
          {
            title: '视频',
            icon: 'shipin',
            router:"/video"
          },
          {
            title: '小影视',
            icon: 'duanshipinhuati',
            router:"/Smallvideo"
          },
          {
            title: '播出',
            icon: '16shipin-1',
            router:"/broadcast"
          },
          {
            title: '我的',
            icon: 'wode',
            router:"/my"
          }
        ],

    };
  },

};
</script>

<style lang="less" scoped>
.HomeFooter {
  background: #fff;
  width: 100%;
  height: 48px;
  border-top: 1px solid black;
  position: fixed;
  left: 0;
  bottom: 0;
  display: flex;
  justify-content: space-around;
  align-items: center;
  z-index: 1;
  &>div {
    height: 100%;
    width: calc(100% / 5);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    .iconfont {
        font-size: 20px;
    }
    & span:last-child {
        font-size: 12px;
    }
  }
  .router-link-active {
    color: red;
  }
}
</style>

# 大神

<template>
  <div class="wrapper" ref="wrapper">
    <div>
 
     <ul class="content">
        <li v-for="item in data">{{item}}</li>
      </ul>
 
      <div class="bottom-tip">
      <span class="loading-hook">查看更多</span>
     </div> 
 
    <div>
  </div>
</template>
<script>
  import BScroll from 'better-scroll'
  export default {
    data() {
      return {
        data: []
      }
    },
    created() {
      this.loadData()
    },
    methods: {
      loadData() {
        var self = this;
       requestData().then((res) => {
          this.data = res.data.concat(this.data)
          this.$nextTick(() => {
            if (!this.scroll) {
              this.scroll = new Bscroll(this.$refs.wrapper, {    
                pullUpLoad:{
           threshold: -30, // 负值是当上拉到超过低部 30px；正值是距离底部距离时，
          }
              })
              this.scroll.on('touchend', (pos) => {
                // 下拉动作
                if (pos.y > 50) {
                  self.loadData()
                }
              })
              this.scroll.on('pullingUp', (pos) => {
          document.querySelector('.loading-hook').innerText = '加载中...';
          setTimeout(function () {
           // 恢复文本值
           document.querySelector('.loading-hook').innerText = '查看更多';
           // 向列表添加数据
           self.loadData();
          }, 1000);
         }) 
            } else {
                this.scroll.finishPullUp() 
                this.scroll.refresh()
            }
          })
        })
      }
    }
  }
<script>

