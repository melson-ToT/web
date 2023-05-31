# 一. qs 一个轻量的 url 参数转换的 JavaScript 库,使用获取url参数，极其方便

1. https://www.npmjs.com/package/qs

2. qs 一个轻量的 url 参数转换的 JavaScript 库,使用获取url参数，极其方便

3. npm install qs --save

4. B站：https://www.bilibili.com/video/BV13i4y1w7WK/?spm_id_from=333.337.search-card.all.click&vd_source=79ae7e0bf3c2cf0e4adfba5746d57437

5. 在main.js中引入qs，并配置全局

import qs from 'qs'
Vue.use(qs)

6. 在组件中引入 import qs from 'qs'



# 二. qs.stringify() 将对象转成string类型

1. 作用是将对象转 url 的形式

2. 参数是对象

3. 返回值是字符串

4. qs.parse将url参数转成对象形式解析  2. 用qs.stringfy将对象转成string类型传参

let obj = {
  name = 'zhangsan',
  age = 18
}

qs.stringify(obj)
<!-- "name=zhang&age=20" -->


let - obj = {
  name = 'zhangsan',
  age = 18,
  aaa = ['ENF','CHINA']
}

qs.stringify(obj)
<!-- "name=zhangsan&age=18&aaa%5B0%5D=ENF&aaa%5B1%5D=CHINA" -->

<!-- 在实际项目中，如果我们想把 obj 对象转为 url 可识别的参数-->
decodeURL(qs.stringify(obj,opts:{indices:false}))


# 三. qs.parse() qs.parse将url参数转成对象形式
let arr = "name=zhang&age=20"
console.log(qs.parse(arr));
<!-- {name: 'zhang', age: '20'} -->

let url = 'http://www.baidu.com?name=zhang&age=20'
console.log(qs.parse(url));
<!-- {http://www.baidu.com?name: 'zhang', age: '20'} -->



