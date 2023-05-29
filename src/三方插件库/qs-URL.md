# 一. qs 一个轻量的 url 参数转换的 JavaScript 库,使用获取url参数，极其方便

1. https://dayjs.fenxianglu.cn/category/

2. qs 一个轻量的 url 参数转换的 JavaScript 库,使用获取url参数，极其方便

3. npm install qs --save


4.  在main.js中引入qs，并配置全局

import qs as "qs"

//配全局属性配置，在任意组件内可以使用this.$qs获取qs对象 
Vue.prototype.$qs = qs



# 二. qs.stringify()

1. 作用是将对象转 url 的形式

2. 参数是对象

3. 返回值是字符串

let - obj = {
  name = 'zhangsan',
  age = 18
}

qs.stringify(obj)
<!-- "name=zhang&age=20" -->


let - obj = {
  name = 'zhangsan',
  age = 18,
  aaa = ['666','777']
}

qs.stringify(obj)
"name=zhang&age=20&aaa=666&aaa=777"

https://www.bilibili.com/video/BV13i4y1w7WK/?spm_id_from=333.337.search-card.all.click&vd_source=79ae7e0bf3c2cf0e4adfba5746d57437






