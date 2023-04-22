# 一.button按钮特有的属性：

1. 如果在button按钮中加:disabled=""，则不可输入内容

2. 可以设置一个变量在data中，为true和false，在监听属性（watch:{}）中来设置条件，当满足条件时，将:disabled=""中的true和false取反

<body>
    <div id="app">
      <li v-for="(item, index) in list" :key="index" @click="click(item)">{{item}}</li>
      <input type="text" v-model="value">
      <button :disabled="!flag" @click="hanadle">点击事件</button>
    </div>
  </body>
  </html>
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
  <script>
    new Vue({
      el: "#app",
      data: {
        list: [500, 1000, 2000],
        value: '',
        flag: false
      },
      methods: {
        click(item) { //函数传参，将自身的值 = 自身遍历的结果
          this.value = item
        },
      },
      watch: {
        value(n, o) {
          reg = /^[1-9]+[0-9]*$/
          if (reg.test(n)) {
            this.flag = true
          } else {
            this.value = ''
          }
        }
      }
    });
  </script>
  