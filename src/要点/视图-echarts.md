
# 一.echarts-视图

1. 在百度内 -> echarts

2. 点击 百度echarts

3. 点击 echarts.apache.org

4. 点击 高级

5. 点击 继续前往

6. 点击 示例


# 二.antv-视图

1. 在百度内 -> antv

2. 点击 AntV | 蚂蚁数据可视化

3. 点击 G2

4. 点击 图标示例


# 三.highcharts-视图

1. 在百度内 -> highcharts

2. 点击 ...完美支持移动端、图表类型丰富的 HTML5 交互...官方

3. 点击 高级

4. 点击 继续前往

5. 点击 查看实例



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



#  六. 配置项

1. 在 文档-> 配置项手册中 -> 添加或更改属性

2.  radius: [50, 250],50表示：内圈的半径，250表示：外圈的半径

3. 案例：如果 mounted()生命周期中，有两个或以上的视图代码，那么会有相同的属性名重合 ，在使用时，只需要更改为不同的名字，就可以使用了
<template>
  <div class="box1">
    <div id="box2"></div>
    <div id="box3"></div>
    <div id="box4"></div>
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

    var chartDom = document.getElementById("box3");
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

    var chartDo = document.getElementById("box4");
    var myCha = echarts.init(chartDo);
    var optio;

    optio = {
      title: {
        text: "周访问数",
      },
      legend: {
        top: "bottom",
      },
    //   toolbox: {   右上角的按钮，干掉
    //     show: true,
    //     feature: {
    //       mark: { show: true },
    //       dataView: { show: true, readOnly: false },
    //       restore: { show: true },
    //       saveAsImage: { show: true },
    //     },
    //   },
      series: [
        {
          name: "Nightingale Chart",
          type: "pie",
          radius: [50, 250],
          center: ["50%", "50%"],
          roseType: "area",
          itemStyle: {
            borderRadius: 7,
          },
          data: [
            { value: 40, name: "星期 一" },
            { value: 38, name: "星期 二" },
            { value: 32, name: "星期 三" },
            { value: 30, name: "星期 四" },
            { value: 28, name: "星期 五" },
            { value: 26, name: "星期 六" },
            { value: 22, name: "星期 日" },
          ],
        },
      ],
    };

    optio && myCha.setOption(optio);
  },
};
</script>

<style lang="less" scoped>
.box1 {
  width: 100%;
  height: 100%;
  display: flex;
  #box2 {
    width: 500px;
    height: 500px;
  }
  #box3 {
    width: 500px;
    height: 500px;
  }
  #box4 {
    width: 700px;
    height: 600px;
  }
}
</style>