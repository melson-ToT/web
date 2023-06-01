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
<template>
  <div class="login">
    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      class="demo-ruleForm"
    >
      <el-form-item label="账号" prop="username">
        <el-input
          v-model="ruleForm.username"
          placeholder="请输入内容"
        ></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input
          placeholder="请输入密码"
          v-model="ruleForm.password"
          show-password
        ></el-input>
      </el-form-item>
      <div class="bt">
        <el-button type="success" @click="fn">登录</el-button>
        <el-button type="info" @click="fa">重置</el-button>
      </div>
    </el-form>
  </div>
</template>

<script>
import aaa from "../../utils/index";
export default {
  data() {
    return {
      //登录表单的数据绑定对象
      ruleForm: {
        username: "",
        password: "",
      },
      //验证用户名和密码是否合法
      rules: {
        //验证用户名是否合法
        username: [
          { required: true, message: "请输入账号", trigger: "blur" },
          {
            // pattern: /^[a-zA-Z][-_a-zA-Z0-9]{5,12}$/,
            message: "格式有误",
            trigger: "blur",
          },
        ],
        //验证密码是否合法
        password: [
          { required: true, message: "请输入密码", trigger: "blur" },
          {
            // pattern: /^[a-zA-Z][-_a-zA-Z0-9]{5,12}$/,
            message: "格式有误",
            trigger: "blur",
          },
        ],
      },
    };
  },
  methods: {
    fn() {
      aaa({
        method: "POST",
        url: "/api/login",
        params: { age: 1 },
      }).then((res)=>{
        if(res.data.c)
      })
  },
};
</script>

<style lang="less" scoped>
.login {
  width: 100%;
  height: 100%;
  .el-form {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 30px;
    box-sizing: border-box;
    .el-form-item {
      display: flex;
      .el-input {
        width: 218px;
      }
    }
  }
  .bt {
    display: flex;
    justify-content: space-evenly;
  }
}
</style>

S



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


