# 一.class和style的绑定
1. class允许写成对象的形式
2. class对象里面：key表示类名，value表示变量或表达式
3. 类名如果是连字符的，则需要加''号
4. class可以和v-bind：class一起使用，不会被覆盖

案例：
<style>
   .font {
      color: red;
   }
   .big {
     font-size: 50px;
   }   
   .size-w {
      font-weight: 900;
   }
</style>
<body>
   <div id="app">
     <p v-bind:class="{font:show,big:num===1,'size-w':weihht}">hello Vue!</p>
   </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
   const p1 = new Vue({
      el: '#app',
      data: {
         show:true,
         num:1,
         weihht:true
      },
   })
</script>
</html>


