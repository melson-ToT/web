# 一.axios-请求

1. 安装：npm i axios

2. <script src="https://unpkg.com/axios/dist/axios.min.js"/></script>

3. axios:官网  https://github.com/axios/axios
点击右侧-> axios-http.com 点击下面-> 中文 点击-> 起步 点击-> Axios API




# 二.在src文件夹中，的utile文件夹，中建立一个index.js文件

import axios from 'axios'

const ccc = axios.create({
    baseURL:'http://192.168.0.159:8888',
    timeout:5000,
    <!-- timeout:超时时间，不然浏览器一直在转 -->
})

export default aaa


# 三.在src文件夹中，的api文件夹，中建立一个sss.js文件

1. import ccc from '../utile/index.js'

2. export function getaaa (params = {}){
    <!-- getaaa：某个获取请求的方法，params = {}空对象 -->
     return ccc({
      <!-- ccc为：utile/index.js 的ccc-->
       method: 'GET',
       url: '/bit',
       params，
     })
   }

3. export function getbbb (id){
      <!-- getbbb：详情页面获取请求的方法，(id)详情页面的Id -->
     return ccc({
       method: 'GET',
       url: '/bit/${id}',
       params，
     })
   }

4. 在src文件夹中，的api文件夹，中建立一个index.js文件

<!-- 导入api内的sss文件 -->

import sss from '/index.js'
export default {
  sss
  <!-- sss就代表 api内 sss.js文件 内的所有文件-->
}


5. 在main.js中，引入api的index.js文件

import api from 'api/index.js'
Vue.prototype.$api = api


# 四.在main.js 引入

import axios from 'axios'
 
Vue.use(axios)



# 五.组件中

1. 先在utile的index.js文件，建立多个 GET 和 POST 请求方法

2. 在 api 中建立多个域名的后缀，然后引入到 自己的 index.js文件中

3. 在 main.js 引入

4. 在组件中寻找对应的接口


fa(){//详情页面的接口
  this.$api.sss.getaaa(this.getaaa.id,this.getaaa).then(()=>{
    this.list = res.data.tada.not
  })
}

fn(){//列表页面的接口
  this.$api.sss.getaaa.then((res)=>{
    this.list = res.data.tada.not
  })
}


<!--  发起一个post请求 -->
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
<!-- // 在 node.js 用GET请求获取远程图片 -->



axios({
  method: 'get',
  url: 'http://bit.ly/2mTM3nY',
  responseType: 'stream'
})
  .then((response) =>{
    response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
  });
axios(url[, config])
<!-- // 发起一个 GET 请求 (默认请求方式) -->
axios('/user/12345');


