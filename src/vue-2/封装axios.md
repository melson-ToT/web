# 一.命令行中下载axios
npm i axiso


# 二.在vue.config.js内，写入
const { defineConfig } = require("@vue/cli-service");
const URL = 'https://i.maoyan.com/api/'
module.exports = defineConfig({
  transpileDependencies: true,
  devServer:{
    proxy:{
      "/api":{
        target: URL,
        changeOrigin:true,
        pathRewrite:{
          '^/api':''
        }
      }
    }
  }
});



# 三.在ulils文件中创建一个文件为api的文件夹，在api的文件夹中创建一个index.js文件

import axios from 'axios'
export function getHotList(){
    return axios({
      url:'/api/mmdb/movie/v3/list/hot.json',
      method: 'get',
      params:{
        ct: '广州',
        ci: 20,
        channelId: 4
      }
    })
}



# 四.在对应的组件的方法中，放入方法中，再讲方法放入生命周期，引入写好的文件----import { getHotList } from "@/api"; 
<script>
// import HomeFavorable from "./HomeFavorable.vue";
// import HomeList from "./HomeList";
import { getHotList } from "@/api";    引入文件
export default {
  // name: "HomeWellreceived",

  // data() {
  //   return {
  //     hotList: [],
  //   };
  // },

  created() {
    this.getHot();
  },

  methods: {
    getHot() {
      getHotList().then((res) => {
        this.hotList = res.data.data.hot;
        console.log(this.hotList);
      });
    },
  },
  // components: {
  //   HomeFavorable,
  //   HomeList,
  // },
};
</script>


# 五.将对象转为字符串模式
   params {a:10,b:20}   >>>>  str "?a=10&b=20"

      const http = {
        get(url,params){
          if(params){
            const arr = Object.keys(params) //arr["a","b"]
            const arr2 = arr.map(item =>item + "=" + params[item])
            const str = "?" + arr2.join("$")
            url +=str
          }
          return fetch(BASE_URL + url).then((response)=>response.jion()).then((res)=>{
            if(res.status === 0){
              return res
            }
          })
        }
      }
       
