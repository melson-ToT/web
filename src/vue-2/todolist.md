# 一.e.target.value
1. e.target.value:是获取触发事件对象的目标，也就是绑定事件的元素
2. filter() 方法创建一个新的数组,不会改变原数组
   this.list = this.list.filter((value)=>value!=item)   
   当前元素的list = 当前元素的list.filter((value)=>value!=item) 


# 二.点击按钮，使input框的内容放入下面的ul标签中，再点击ul中的相应的li，使其删除
思路：
1. 将input进行数据绑定，v-model绑定 = 数据的行参aaa
2. 将数据的行参放置到Vue的data中，因为还没有输入内容，所以行参为空：aaa:'',
3. 将ul的li标签进行v-for遍历，遍历list
4. 将list放置到Vue的data中，因为input还没有输入值的，所以list的数组为空：''
5. 点击button按钮，将点击事件on:click = 一个函数
6. 将函数方法放入Vue的方法中（methods）
7. input框输入后，点击button，函数内：将当前输入的内容（this.行参）push到ul的li内（this.list）
8. 这样input框的内容就和ul的li进行了数据绑定
9. input框输入一次内容，点击一下button按钮，就将input框的内容push到ul的li内
10. this.aaa = ''，再将input的内容清空
11. 在每个li的后面加一个button按钮，内容写删除
12. button按钮内加v-on:click事件，事件 = 函数（v-for遍历的值）
13. 当点击button按钮，this.list = this.list.filter((value)=>value!=item)
                     当前元素的list = 当前元素的list.filter((value)=>value!=item)

<body>
   <div id="app">
      <input type="text" v-model="aaa">
      <button v-on:click="Click">添加</button>
      <ul>
         <li v-for="item in list">{{item}}-<button v-on:click="del(item)">删除</button></li>
      </ul>
   </div>
   </body>
   <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
   <script>
     const p3 = new Vue({
       el:'#app',
       data:{
         list:[],
         aaa:''
       },
       methods:{  
         Click(){
            this.list.push(this.aaa)
            this.aaa = ''
         },
         del(item){
            this.list = this.list.filter((value)=>value!=item)
         }
       }
     })
   </script>
   </html>