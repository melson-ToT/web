# 一.Better-Scroll 2.0插件
1. 移动端和PC端（上拉加载、下拉加载、鼠标滚轮、放大缩小、移动缩放、轮播图、滚动视觉差，放大镜...）事件，谷歌搜索  Better-Scroll 2.0

2. 官网：https://Better-Scroll.github.io/docs/zh-CH/

3. 点击 Getting Started -> 进入，点击右上角--选择语言

4. 主要用于列表的滚动，

5. 通过子元素在父元素里面，改变transiform的translate的值，进行平移

6. 满足的条件：
            1.有父元素和子元素
            2.父元素必须要有明确的宽高
            3.子元素只能有一个
#           4.如果子元素的ul有一个元素与ul平齐，则外面套一个盒子（子元素的ul的css加：overflow: hidden;）
              如果子元素的ul没有元素与ul平齐，则直接用ul的父元素当父元素，（ul的父元素css加：overflow: auto;;）

7. 安装：npm i Better-Scroll --save
        （上拉加载、下拉加载、鼠标滚轮、放大缩小、移动缩放、轮播图、滚动视觉差，放大镜...）事件，都能实现

       （不能安装 ->npm i @Better-Scroll/core --save）
         因为这个只能做下拉加载

8. 在main.js中，看一下有没有

9. 引入 import BetterScroll from "better-scroll"; 那个组件用，就那个组件中引入

10. 创建一个实例对象：new BetterScroll('.wrapper',{})
                     1.创建实例对象，添加滚动

                     2.需要写在数据请求到之后的：（因为li的v-for没有遍历之前，子元素是没有高度的）
                                             BetterScroll的实例，必须放置在项目挂载后 mounted(){} 生命周期钩子内
                            

                     3.里面的参1：父元素的class名（是ul和此组件的中间加一个div，取class名：父元素），
                                 再将ul放入父元素中,因为在ul和p标签平齐，子元素只能有一个，所以，外面再套一个盒子
<template>
  <div class="HomeFavorable">
    <p class="hello">最受好评电影</p>
    <div class="wrapper">
      <ul>
        <li v-for="item in hotList" :key="item.id">
          <img :src="item.img" alt="" />
          <i>观众评分&nbsp;{{ item.mk }}</i>
          <span>{{ item.nm }}</span>
        </li>
      </ul>
    </div>
  </div>
</template> 

                   4.再将这个父元素在css中，宽度100%，overflow: hidden;
                     .wrapper {
                       width: 100%;  //防止页面被撑大
                       overflow: hidden;  //防止ul大于父元素
                    }

                    5.里面的参2：{}为配置对象
                                 mounted() {
                                   //BetterScroll的实例，必须放置在项目挂载后 mounted(){加入 observeDOM: true, 版本问题} 生命周期钩子内
                                      new BetterScroll(".home-list", {
                                      observeDOM: true,   //版本问题
                                      startX:0,           //X轴的初始位置是第一张
                                      scrollX:true ,      //X轴可以滑动
                                      scrollY: false,     //Y轴不能滑动
                                      click:true,         //保留点击事件
                                    }
                                   );
                                  },

                     5.此时还是不能滑动，X轴的滚动条失效:

                     6.删除 ul的 overflow-y: auto，改为overflow: hidden;因为用了"better-scroll"，就不用横向的滚动条了


11. 将ul的宽度在css中删除，
                    再将 display: flex ;改为 display: inline-flex;(将块元素的弹性盒子改为内联块状弹性盒子)，
                    再将 overflow: auto;改为 overflow: hidden;
  ul {
    // width: 100%;
    display: inline-flex;
    overflow: hidden;
  }

13. 在 mounted(){} 生命周期钩子内，加一个 this.$nextTick(()=>{}) 的方法，将 new BetterScroll缩写的实例对象放入里面
  mounted() {
    //BetterScroll的实例，必须放置在项目挂载后生命周期钩子内
    this.$nextTick(() => {
      new BetterScroll(".wrapper", {
        observeDOM: true,
        startX: 0,
        scrollY: false,
        scrollX: true,
        click: true,
      });
    });
  },


# 二.this.$nextTick(()=>{}) 的方法
     作用: 将同步转异步，而且比所有的异步后执行
     意义: 在异步阵列内，确保后拿到异步的数据，再执行
     参考: 将同步的代码放入 this.$nextTick(()=>{}) 内，就可以获取异步的数据

    

# 三，案例：左右平移 ----------如果页面左右和上下跑，父元素一定要加：overflow: hidden;
            1.有父元素和子元素
            2.父元素必须要有明确的宽高
            3.子元素只能有一个
            4.如果子元素的ul有一个元素与ul平齐，则外面套一个盒子（子元素的ul的css加：overflow: hidden;）
            5. 父元素必须要有明确的宽高

<template>
  <div class="HomeFavorable">
    <p class="hello">最受好评电影</p>
    <div class="wrapper">
      <ul>
        <li v-for="item in hotList" :key="item.id">
          <img :src="item.img" alt="" />
          <i>观众评分&nbsp;{{ item.mk }}</i>
          <span>{{ item.nm }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import BetterScroll from "better-scroll";
export default {
  name: "HomeFavorable",
  props: ["hotList"],
  mounted() {
    //BetterScroll的实例，必须放置在项目挂载后生命周期钩子内
    this.$nextTick(() => {
      //在 mounted(){} 生命周期钩子内，加一个 this.$nextTick(()=>{}) 的方法，将 new BetterScroll缩写的实例对象放入里面
      new BetterScroll(".wrapper", {
        observeDOM: true,
        startX: 0,
        scrollX: true,
        scrollY: false,
        click: true,
      });
    });
  },
  methods: {},
};
</script>

<style lang="less" scoped>
.HomeFavorable {
  width: 100%;
  height: 205px;
  padding: 12px;
  box-sizing: border-box;
  .hello {
    font-size: 14px;
    color: #333;
    margin-bottom: 12px 15px;
  }
  .wrapper {
    width: 100%; //父元素必须要有明确的宽高
    overflow: hidden; 
    ul {
      // width: 100%;
      //将ul的宽度在css中删除，
      height: 150px;
      display: inline-flex;
      //再将 display: flex ;改为 display: inline-flex;(将块元素的弹性盒子改为内联块状弹性盒子)
      // overflow: auto;
      overflow: hidden;
      //删除 ul的 overflow: auto，改为overflow: hidden;因为用了"better-scroll"，就不用横向的滚动条了
      li {
        width: 85px;
        height: 150px;
        background: #fff;
        list-style: none;
        flex-shrink: 0;
        margin-right: 10px;
        position: relative;
        img {
          width: 85px;
          height: 121px;
          display: block;
        }
        span {
          width: 85px;
          height: 10px;
          font-size: 10px;
          line-height: 10px;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
        }
        i {
          position: absolute;
          top: 100px;
          left: 5px;
          font-size: 8px;
          color: #faaf00;
          font-weight: 600;
          font-style: normal;
        }
      }
      &:last-child {
        margin-right: 0;
      }
    }
  }
}
</style>


                                