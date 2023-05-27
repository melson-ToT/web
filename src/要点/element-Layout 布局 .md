

# 一.element-Layout 布局

1. Element Ui ,地址：https://element.eleme.io/#/zh

2. vue2 项目安装：npm i element-ui -S

3. 在main.js 中引入：
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI);

4. 在 element 找到 Layout 布局，辅助到组件的 html中



# 二.element-Layout 布局 的使用

1. 修改元素的宽度和高度，宽度自适应
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }

2. 屏幕设置对消宽度
body {
  min-width: 1200px;
}

3. 案例：
<template>
  <div class="father">
    <div class="shang"></div>
    <div class="xia">
      <ul></ul>
      <div class="box">
        <el-row :gutter="20">
          <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
          <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
          <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
          <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
          <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="less" scoped>
.father {
  width: 100%;
  height: 100%;
  .shang {
    width: 100%;
    height: 150px;
    background: red;
  }
  .xia {
    width: 100%;
    height: calc(100% - 150px);
    display: flex;
    ul {
      width: 300px;
      height: 100%;
      background: blue;
    }
    .box {
      width: calc(100% - 300px);
      height: 100%;
      padding: 20px;
      .el-row {
        margin: 20px;
        &:last-child {
          margin-bottom: 0;
        }
      }
      .el-col {
        border-radius: 4px;

      }
      .bg-purple-dark {
        background: #99a9bf;
      }
      .bg-purple {
        background: #d3dce6;
      }
      .bg-purple-light {
        background: #e5e9f2;
      }
      .grid-content {
        border-radius: 4px;
        height: 360px;
      }
      .row-bg {
        padding: 10px 0;
        background-color: #f9fafc;
      }
    }
  }
}
</style>
