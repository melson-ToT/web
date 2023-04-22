# 一.面向对象class写法:
1. 混合开发 = 构造函数 + 构造函数原形 + 执行函数
如：
<script>
  function Fan(){
    this.name = 'zhangsan'
  }
  Fan.prototype.init = function(){
    'lisi'
  }
  let p1 = new Fan()
  p1.init()
  console.log(p1)//Fan {name: "zhangsan"}
  console.log(p1.init)//ƒ (){'lisi'}
</script>

2. class开发 = (class 构造函数名 + 构造函数原形) +执行函数
<script>
  class Fan{
    constructor(){
      this.name = 'zhangsan'
    }
    init(){
      'lisi'
    }
  }
  let p1 = new Fan()
  p1.init()
  console.log(p1)//Fan {name: "zhangsan"}
  console.log(p1.init)//ƒ (){'lisi'}
</script>

# 二.面向对象class开发的放大镜效果
<style>
  * {
    margin: 0;
    padding: 0;
  }

  .father {
    margin: 50px 0 0 50px;
  }

  .box {
    width: 300px;
    height: 300px;
    float: left;
    position: relative;
  }

  .xiaotu {
    width: 100%;
    height: 100%;
  }

  .xijing {
    width: 200px;
    height: 200px;
    background-color: blue;
    opacity: 0.3;
    position: absolute;
    top: 0;
    left: 0;
    visibility: hidden;
  }

  .dajing {
    width: 400px;
    height: 400px;
    position: relative;
    overflow: hidden;
    float: left;
  }

  .datu {
    width: 600px;
    height: 600px;
    position: absolute;
    top: 0;
    left: 0;
  }
</style>

<body>
  <div class="father">
    <div class="box">
      <img src="../img/女好骚.png" alt="" class="xiaotu">
      <div class="xijing"></div>
    </div>
    <div class="dajing">
      <img src="../img/女好骚.png" alt="" class="datu">
    </div>
  </div>
</body>

</html>

</html>
<script>
  class Fath {
    constructor() {
      this.father = document.querySelector('.father')
      this.box = document.querySelector('.box')
      this.xiaotu = document.querySelector('.xiaotu')
      this.xijing = document.querySelector('.xijing')
      this.dajing = document.querySelector('.dajing')
      this.datu = document.querySelector('.datu')
    }
    init() {
      this.box.onmouseenter = () => {
        this.xijing.style.visibility = 'visible'
        this.box.onmousemove = (e) => {
          let leftvalue = e.clientX - this.father.offsetLeft - this.xijing.offsetWidth / 2
          let topvalue = e.clientY - this.father.offsetTop - this.xijing.offsetHeight / 2
          if (leftvalue <= 0) {
            leftvalue = 0
          } else if (leftvalue >= this.xiaotu.offsetWidth - this.xijing.offsetWidth) {
            leftvalue = this.xiaotu.offsetWidth - this.xijing.offsetWidth
          }
          if (topvalue <= 0) {
            topvalue = 0
          } else if (topvalue >= this.xiaotu.offsetHeight - this.xijing.offsetHeight) {
            topvalue = this.xiaotu.offsetHeight - this.xijing.offsetHeight
          }
          this.xijing.style.left = leftvalue + 'px'
          this.xijing.style.top = topvalue + 'px'
          this.datu.style.left = -leftvalue * (this.datu.offsetWidth / this.xiaotu.offsetWidth) + 'px'
          this.datu.style.top = -topvalue * (this.datu.offsetWidth / this.xiaotu.offsetWidth) + 'px'
        }
      }
      this.box.onmouseleave = () => {
        this.xijing.style.visibility = 'hidden'
      }
    }
  }
  new Fath().init()
</script>