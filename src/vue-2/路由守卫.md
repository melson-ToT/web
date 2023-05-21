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