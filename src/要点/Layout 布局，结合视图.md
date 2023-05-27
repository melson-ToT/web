

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
          <!-- el-col 所有的 :span=""加起来的总和为24-->
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



# 三. echarts-视图

1. 在百度内 -> echarts

2. 点击 百度echarts

3. 点击 echarts.apache.org

4. 点击 高级

5. 点击 继续前往

6. 点击 示例



# 四. 安装 echarts

1. npm install echarts --save

2. 那个组件需要使用，就在该组件中的 <script> 内 引入

3. import * as echarts from 'echarts';
案例：
<script>
import * as echarts from 'echarts';
export default {

};
</script>




# 五.使用 echarts-视图

1. 组件内直接使用，和引入
<script>
import * as echarts from 'echarts';
export default {

};
</script>

2. 点击该视图

3. 点击完整代码，

4. 将对应的 视图的 代码，放入 mounted生命周期中

5. 在html中，自身元素，并且一定要用: # id ,不能用 class
<div id="shitu"></div>

6. 如果 mounted()生命周期中，有两个或以上的视图代码，那么会有相同的var myChart ，在使用时，只需要将myChart改一个不同的名字，就可以
案例：
var myChart = echarts.init(document.getElementById("shitu"));
var myChar = echarts.init(chartDom);

7. 案例：
<template>
  <div class="box1">
    <div id="box2"></div>
    <div id="box3"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  mounted() {
    var myChart = echarts.init(document.getElementById("box2"));
    // 绘制图表
    myChart.setOption({
      title: {
        text: "ECharts 入门示例",
      },
      tooltip: {},
      xAxis: {
        data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
      },
      yAxis: {},
      series: [
        {
          name: "销量",
          type: "bar",
          data: [5, 20, 36, 10, 10, 20],
        },
      ],
    });

    var chartDom = document.getElementById("box3");
    var myChar = echarts.init(chartDom);
    var option;

    option = {
      title: [
        {
          text: "Tangential Polar Bar Label Position (middle)",
        },
      ],
      polar: {
        radius: [30, "80%"],
      },
      angleAxis: {
        max: 4,
        startAngle: 75,
      },
      radiusAxis: {
        type: "category",
        data: ["a", "b", "c", "d"],
      },
      tooltip: {},
      series: {
        type: "bar",
        data: [2, 1.2, 2.4, 3.6],
        coordinateSystem: "polar",
        label: {
          show: true,
          position: "middle",
          formatter: "{b}: {c}",
        },
      },
    };

    option && myChar.setOption(option);
  },
};
</script>

<style lang="less" scoped>
.box1 {
  width: 100%;
  height: 100%;
  #box2 {
    width: 500px;
    height: 500px;
  }
  #box3 {
    width: 500px;
    height: 500px;
  }
}
</style>








# 六. Layout 布局，结合视图

1. echarts 的 <div id="box1"></div>，直接写入<el-col>的<div>内，命名一个id
<el-col :span="6"><div class="grid-content bg-purple" id="box1"></div></el-col>

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
          <el-col :span="6"><div class="grid-content bg-purple" id="box1"></div></el-col>
          <el-col :span="6"><div class="grid-content bg-purple" id="box2"></div></el-col>
          <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  mounted(){
    var myChart = echarts.init(document.getElementById("box1"));
    // 绘制图表
    myChart.setOption({
      title: {
        text: "柱形图",
      },
      tooltip: {},
      xAxis: {
        data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
      },
      yAxis: {},
      series: [
        {
          name: "销量",
          type: "bar",
          data: [5, 20, 36, 10, 10, 20],
        },
      ],
    });
     var chartDom = document.getElementById("box2");
    var myChar = echarts.init(chartDom);
    var option;

    option = {
      title: [
        {
          text: "饼形图",
        },
      ],
      polar: {
        radius: [30, "80%"],
      },
      angleAxis: {
        max: 4,
        startAngle: 75,
      },
      radiusAxis: {
        type: "category",
        data: ["a", "b", "c", "d"],
      },
      tooltip: {},
      series: {
        type: "bar",
        data: [2, 1.2, 2.4, 3.6],
        coordinateSystem: "polar",
        label: {
          show: true,
          position: "middle",
          formatter: "{b}: {c}",
        },
      },
    };

    option && myChar.setOption(option);
  }
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



# 七. 视图，请求数据


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
          <el-col :span="6"
            ><div class="grid-content bg-purple"></div
          ></el-col>
          <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  mounted() {
    var myChart = echarts.init(document.getElementById("box1"));
    // 绘制图表
    myChart.setOption({
      title: {
        text: "柱形图",
      },
      tooltip: {},
      xAxis: {
        data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
      },
      yAxis: {},
      series: [
        {
          name: "销量",
          type: "bar",
          data: [5, 20, 36, 10, 10, 20],
        },
      ],
    });
   
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
