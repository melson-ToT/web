# 一.api请求

export function simpleData (data){
    return fetch.request({
        url:"/data/simpleData",
        method:"get",
        params:{
            ...data
        }
    })
}


# 二.echarts 视图，请求封装
<template>
  <div class="father">
    <div class="shang"></div>
    <div class="xia">
      <ul></ul>
      <div class="box">
        <el-row :gutter="20">
          <el-col :span="6"
            ><div class="grid-content bg-purple" id="box1"></div
          ></el-col>
          <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
          <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import { simpleData } from "../../../api/echarts";
export default {
  data() {
    this.myChart = null;  //先设 myChart 为没有
    return {
      list: [],
    };
  },
  mounted() {
    this.myChart = echarts.init(document.getElementById("box1")); //获取 box1
    this.getData();//将方法放入生命周期
  },
  methods: {
    setData(list) { //将 list 代入
      // 绘制图表
      this.myChart.setOption({  视图的代码
        title: {
          text: "柱形图",
        },
        tooltip: {},
        xAxis: {
          data: list.map((item) => item.x), //遍历 list 中 的 data 的 X
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: list.map((item) => item.val),//遍历 list 中 的 data 的 val
          },
        ],
      });
    },

    getData() {
      simpleData().then((res) => {
        this.setData(res.data) //将 setData 代入到  getData 中
      });
    },
  },
};
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




