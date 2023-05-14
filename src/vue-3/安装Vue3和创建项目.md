# 一.vue3 项目创建：
1. git clone https://github.com/melson-ToT/vue-3.git

2. cd vue-3

3. 安装：npm i -g @vue/cli

4. vue create vue-3

5. 不要选择(vue3/vue2),选择 Manually select features

6. 选择：Babel、Router、Vuex、CSS Pre-processors、Linter / Formatter

7. 选择:3x

8. ? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) n(默认)选择哈希路由

9. > Sass/SCSS (with dart-sass) less,sass 都可以

# 10. > ESLint with error prevention only----不要报错
      ESLint + Airbnb config
      ESLint + Standard config
      ESLint + Prettier

# 11. >(*) Lint on save  ----这个
       ( ) Lint and fix on commit

# 12. > In dedicated config files  ----这个
        In package.json

13. ? Save this as a preset for future projects? (y/N) n

14. cd vue-3



# 二.vue2 项目创建：
1. git clone https://github.com/melson-ToT/vue-3.git

2. cd vue-2

3. 安装：npm i -g @vue/cli

4. vue create vue-2

5. 不要选择(vue3/vue2),选择 Manually select features

6. 选择：Babel、Router、Vuex、CSS Pre-processors、Linter / Formatter

7. 选择:2x

8. ? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) n(默认)选择哈希路由

9. > Sass/SCSS (with dart-sass) less,sass 都可以

# 10. > ESLint with error prevention only----不要报错
      ESLint + Airbnb config
      ESLint + Standard config
      ESLint + Prettier

# 11. >(*) Lint on save  ----这个
       ( ) Lint and fix on commit

# 12. > In dedicated config files  ----这个
        In package.json

13. ? Save this as a preset for future projects? (y/N) n

14. cd vue-3



# 三.单页面切换：
1. 父组件
<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
</template>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>


2. 子组件 1
<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>

3. 孙组件
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <!-- 在子组件中， msg 使用了 props 接收，所以 {{ msg }} 可以直接输出 props 里接收的内容。 而没在 props 里接收的内容，全部都放到了 $attrs 里， -->
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-router" target="_blank" rel="noopener">router</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-vuex" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>


4. 子组件 2
<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>


# 五. <HelloWorld msg="属性"/>
<!-- 在子组件中， msg 使用了 props 接收，所以 {{ msg }} 可以直接输出 props 里接收的内容。 而没在 props 里接收的内容，全部都放到了 $attrs 里， -->

attrs在 template 中的用法
在前面简单的例子里其实已经大概知道 attrs 在 template 的用法。但 Vue3 中 template 不再要求只有一个根元素了。所以 attrs 在 template 中分2种情况使用。


只有1个根元素的情况下，子组件中，没被 props 接收的属性，都会绑定在根元素上。

<!-- 父组件 ParentCom.vue -->
<template>
  <ChildCom
    msg="雷猴"
    data="123"
    name="鲨鱼辣椒"
    style="color: red;"
  />
</template>

<script setup>
import ChildCom from './ChildCom.vue'
</script>



<!-- 子组件 ChildCom.vue -->
<template>
  <div>
    {{ msg }}
  </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String
  }
})
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）

可以看到，没被 props 接收的属性都被绑定到根元素上了。

连 style 里传入的样式也被执行，文字变成红色了。



如果此时我们想在页面输出 name 的值，可以在子组件中这样操作

<!-- 这里省略 父组件代码 ...... -->



<!-- 子组件 ChildCom.vue -->
<template>
  <div>
    {{ $attrs.name }}
  </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String
  }
})
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）

使用 $attrs.xxx ，这里的 xxx 是对应的属性名。



有2个根元素的情况下
当子组件有2个根元素时，没被 props 接收的属性不会绑定到子组件的元素上。

<!-- 父组件 ParentCom.vue -->
<template>
  <ChildCom
    msg="雷猴"
    data="123"
    name="鲨鱼辣椒"
    style="color: red;"
  />
</template>

<script setup>
import ChildCom from './ChildCom.vue'
</script>



<!-- 子组件 ChildCom.vue -->
<template>
  <div>
    {{ msg }}
  </div>
  <div>
    {{ msg }}
  </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String
  }
})
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）

此时连父组件传入是 style 样式都不生效了。

如果我们此时希望第二个元素绑定所有没被 props 接收的属性，可以使用 v-bind="$attrs" 的方法实现

<!-- 父组件 ParentCom.vue -->
<template>
  <ChildCom
    msg="雷猴"
    data="123"
    name="鲨鱼辣椒"
    style="color: red;"
  />
</template>

<script setup>
import ChildCom from './ChildCom.vue'
</script>



<!-- 子组件 ChildCom.vue -->
<template>
  <div>
    {{ msg }}
  </div>
  <div v-bind="$attrs">
    {{ msg }}
  </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String
  }
})
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）

注意第二个元素，使用了 v-bind="$attrs" 绑定了所有没被 props 接收的属性。



如果只希望绑定部分属性，可以单独写

<!-- 这里省略 父组件代码 ...... -->



<!-- 子组件 ChildCom.vue -->
<template>
  <div>
    {{ msg }}
  </div>
  <div :style="$attrs.style">
    {{ msg }}
  </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String
  }
})
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）





attrs在 js 中的用法
除了在 template 中可以访问到 $attrs ，在 JS 中也可以访问到。



vue 3 其实是兼容大部分 Vue 2 语法的，也就是 Options API 。而 attrs 在 Options APi 和 Composition Api 中的使用方法会稍微有一丢丢区别。而 Composition API 又分为 Vue 3.2 前的语法和 3.2 后的语法。

接下来将分开讨论这3种情况。



Options API
<!-- 父组件 ParentCom.vue -->
<template>
  <ChildCom
    msg="雷猴"
    data="123"
    name="鲨鱼辣椒"
    style="color: red;"
  />
</template>

<script setup>
import ChildCom from './ChildCom.vue'
</script>



<!-- 子组件 ChildCom.vue 暂不关注 template 部分 -->
<script>
export default {
  props: {
    msg: {
      type: String
    }
  },
  mounted() {
    console.log(this.$attrs)
  }
}
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）

此时控制台会输出没被 props 接收的属性。



Composition API 3.0的语法
<!-- 父组件 ParentCom.vue -->
<template>
  <ChildCom
    msg="雷猴"
    data="123"
    name="鲨鱼辣椒"
    style="color: red;"
  />
</template>

<script setup>
import ChildCom from './ChildCom.vue'
</script>



<!-- 子组件 ChildCom.vue 暂不关注 template 部分 -->
<script>
export default {
  props: {
    msg: {
      type: String
    }
  },
  setup(props, context) {
    console.log('props: ', props)
    console.log('attrs: ', context.attrs)
  }
}
</script>
Vue3 - $attrs 的几种用法（1个或多个根元素、Options API 和 Composition API）

Vue 3.2 前的写法，需要在 setup 方法里接收2个参数，而 attrs 就在 context 参数里。



Composition API 3.2的语法
Vue 3.2 后的语法，可以在 <script> 标签上添加 setup 属性。所以在代码里就不需要再调用 setup 方法了。

在这种情况下，props 成了默认的全局方法，而 attrs 则需要另外引入。

<!-- 父组件 ParentCom.vue -->
<template>
  <ChildCom
    msg="雷猴"
    data="123"
    name="鲨鱼辣椒"
    style="color: red;"
  />
</template>

<script setup>
import ChildCom from './ChildCom.vue'
</script>



<!-- 子组件 ChildCom.vue 暂不关注 template 部分 -->
<script setup>
import { useAttrs } from 'vue'

const props = defineProps({
  msg: {
    type: String
  }
})

const attrs = useAttrs()

console.log('props: ', props)
console.log('attrs: ', attrs)
</script>
08



需要引入 vue 中的 useAttrs ，在调用 useAttrs 后会返回当前未被 props 接收的属性。

重点是以下两句。

import { useAttrs } from 'vue'
const attrs = useAttrs()
之后在 js 代码里就可以使用 attrs.xxx 获取对应的属性值了。