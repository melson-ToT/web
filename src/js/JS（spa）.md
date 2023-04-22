  # 一.什么是路由和前端路由(强调的是概念)
   1.路由（英文：router）就是对应关系
   2.路由的概念来源于服务端，在服务端中路由描述的是 URL 与处理函数之间的映射关系
   3.前端路由就是浏览器地址栏中的 URL与所见网页的对应关系(Hash地址与组件之间的对应关系)
   组件（components）：指对具体的某个功能进行封装(html+css+js)，来达到组件复用，提高开发效率。
 
 
  # 二.SPA(single page application:单页面应用)
   1.SPA（single page application），翻译过来就是单页应用，SPA是一种网络应用程序或网站的模型， 它通过动态重写当前页面来与用户交互，这种方法避免了页面之间切换打断用户体验。
   2.在单页应用中，所有必要的代码（HTML、JavaScript和CSS）都通过单个页面的加载而检索，或者根据需要（通常是为响应用户操作）动态装载适当的资源并添加到页面
   3.始终只有一个html页面，页面在任何时间点都不会重新加载(刷新)，也不会将控制转移到其他页面
 
 
  # 三.如何实现前端路由？要实现前端路由，需要解决两个核心：
   - 如何改变 URL(统一资源定位符 - 完整的域名) 却不引起页面刷新？ - a标签，表单
   - 如何检测 URL 变化了？    onhashchange事件
 
 
  # 四.实现路由的方式有两种:
   - 依赖 hash 的改变(锚点)
   - 依赖历史记录(history)

  # 五.案例
  <style>
  *{
    margin: 0;
    padding: 0;
  }
  html,body,.father{
    width: 100%;
    height: 100%;
  }
  .father {
    display: flex;
    flex-direction: column;
  }
  .top {
    width: 100%;
    height: 100px;
    background-color: red;
  }
  .floop {
    width: 100%;
    height: calc(100% - 100px);
    background-color: aqua;
    display: flex;
  }
  .left {
    width: 200px;
    height: 100%;
    background-color: beige;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
  }
  .left>a {
    font-size: 20px;
    margin-bottom: 10px;
    text-decoration: none;
  }
  .right {
    width: calc(100% - 200px);
    height: 100%;
    background-color: burlywood;
  }
</style>
<body> 
  <div class="father">
    <div class="top"></div>
    <div class="floop">
      <div class="left">
        <a href="#/zhuce">注册页面的显示</a>
        <a href="#/gouwu">购物页面的显示</a>
        <a href="#/youxi">游戏页面的显示</a>
        <a href="#/shengguo">生活页面的显示</a>
      </div>
      <div class="right"></div>
    </div>
  </div>
</body>
</html>
</html>
<script>
  const right = document.querySelector('.right')  1.取右边的元素
  window.addEventListener('hashchange',fn)  2.当单页面的哈希值发生改变时
  function fn(){            
    switch(location.hash){  3.哈希值为：
      case '#/zhuce':right.innerHTML = '注册页面的显示,111111111111'
      break
            3.1  哈希值为：#/zhuce时，右边的内容为：'注册页面的显示,111111111111'

      case '#/gouwu':right.innerHTML = '购物页面的显示,222222222222'
      break
            3.2  哈希值为：#/gouwu时，右边的内容为：'购物页面的显示,222222222222'
            
      case '#/youxi':right.innerHTML = '游戏页面的显示,333333333333'
      break
            3.3  哈希值为：#/youxi时，右边的内容为：'游戏页面的显示,333333333333'

      case '#/shengguo':right.innerHTML = '生活页面的显示,4444444444'
      break
            3.4  哈希值为：#/shengguo时，右边的内容为：'生活页面的显示,4444444444'

      default :right.innerHTML = '404 Not Found'
    }
            3.5  如果都不是，右边的内容为：'404 Not Found'
  }
    fn()   4. 一开始触发一次事件里面的函数
</script>
