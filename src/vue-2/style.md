# 一.绑定内联样式
1. v-bind:style="" 可以简写为：  :style=""
2. :style=""也允许写成对象的格式，key还是CSS类名，value是变量或者表达式
3. style=""内，color:'red'，red加引号，fontSize: '50px'
4. fontSize: '50px'，由font-size连字符，变为驼峰fontSize
5. 平移:transform:'translate('+ res+'px),将p标签的某个属性变为变量放入data中，点击时让变量（+=这个变量）

<body>
   <div id="app">
     <p :style="{color:'red',fontSize: '50px',transform:'translate('+ res+'px)'}">hello Vue!</p>
     <button @click="res += 50">平移</button>
   </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
   const p1 = new Vue({
      el: '#app',
      data: {
         res:50
      },
   })
</script>
</html>