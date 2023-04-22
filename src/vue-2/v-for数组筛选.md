# 一.v-for循环的嵌套：
<body>
  <div id="app">
    <ul>
      <li v-for="(item,index) in list" :key="index">
        <span v-for="(value,index) in item" :key="index">{{value}}</span>
        <!-- 将li内的item值作为span的循环对象 -->
      </li>
    </ul>
  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const p1 = new Vue({
    el: '#app',
    data:{
         list:[
          [1,2,3,4],
          [5,6,7,8]
        ]   
      },
  })
</script>
</html>


# 二.如果v-for遍历的对象是数字，则会数字从1~到对象的所有数字，都显示出来
   <li v-for="(item,index) in 8" :key="index">{{item}}</li>
   为：12345678


# 三.v-for与v-if一起使用时
1. 最好不要在同一个元素上使用v-for和v-if
<li v-for="(item,index) in list" v-if="item % 2" :key="index">{{item}}</li>

2. 同一个元素上使用v-for和v-if，v-for的优先级更高
   <!-- 先渲染再判断，导致不必要的开销，消耗性能 -->

3. 解决办法：通过计算属性的方法
<body>
  <div id="app">
    <ul>
      <li v-for="(item,index) in addlist" :key="index">{{item}}</li>
    </ul>
  </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const p1 = new Vue({
    el: '#app',
    data:{
         list:[1,2,3,4,5,6,7]   
      },
    computed:{
      addlist(){
        return this.list.filter((item)=>item % 2)
      }
    }
  })
</script>
</html>


# 四.当判断的田间和item无关的时候，可以将v-if放到ul上