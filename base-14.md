### Vue 完整版和运行时版
1. 完整版
- vue.js
~~~
https://cdn.bootcdn.net/ajax/libs/vue/2.6.10/vue.min.js
~~~
2. 运行时版
- vue.runtime.js
~~~
https://cdn.bootcdn.net/ajax/libs/vue/2.6.10/vue.runtime.min.js
~~~

### 两者的区别和联系
为什么会有两个版本，他们之间使用有什么区别。

简单来说，vue.js 是完整版的 Vue，拥有全部的组件（如 compiler）,而非完整版则没有。

正因为非完整版，没有 compiler（用于编译的） 组件，非完整版的体积要小完整版的40%，非常适合给客户浏览器更快地加载使用，Vue 默认就是使用非完整版的。

但也正因为没有 compiler，非完整版是不能使用 template ，需要使用 h 函数来渲染页面，开发体验特别糟糕。

但是，由于可以用 webpack 来打包，vue-loader 负责把 template 转换成 h 函数，实现即使用非完整版，也能按完整版的开发流程实现。

### template 和 render
template是Vue单文件组件中负责视图的部分
~~~html
<template>
  <div class="red">
    {{ n }}
    <button @click="add">+1</button>
  </div>
</template>
~~~

#### render是用于渲染template的
~~~js
import demo from './demo.vue'
new Vue({
  el: '#app',
  render(h) {
    return h(demo)
  }
~~~

### 使用 CodeSandbox 写 Vue 代码
> https://codesandbox.io/s/kind-heisenberg-wjxpe?file=/src/main.js

使用以上的网址可以直接在Vue的环境下开始工作，不用登录