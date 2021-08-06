## Vue的sync修饰符
在说sync之前，我们需要了解Vue里面的三条规整
1. 组件不能修改 props 外部数据
2. $emit 可以触发事件，并且传递参数
3. $event 可以获取$emit 的参数  

基于以上三条规整，我们可以实现一个子组件改变父组件的数据过程   
建议使用
https://codesandbox.io/
来验证

### child.vue
~~~xml
<template>
  <div class="child">
    这里是Child层
    <br />
    n的值：{{ n }}
    <button @click="$emit('update:n', n - 1)">
      <span>改变n</span>
    </button>
  </div>
</template>

<script>
export default { props: ["n"] };
</script>

<style>
.child {
  border: 1px solid green;
}
</style>
~~~

### father.vue
~~~xml
<template>
  <div class="father">
    这里是Father层
    <br/>
    最终结果：{{result}}
    <Child :n.sync="result"/>
  </div>
</template>

<script>
    import Child from './Child.vue'
    export default {
        data(){
            return {result:250}
        },
    components: { Child: Child }
    }
</script>

<style>
.father {
  border: 2px solid green;
  padding:10px
}
</style>
~~~

我们可以看到，点击子组件里面的按钮时候，父组件内部的n的值也相应发生了改变

## sync
在father.vue里面
~~~xml
<Child :n="result" v-on:update:n="result = $event"/>
~~~
这一句，可以简写为
~~~xml
<Child :n.sync="result"/>
~~~
**sync** 就是Vue作者发明的语法糖，让我们省去了后面v-on的语句
