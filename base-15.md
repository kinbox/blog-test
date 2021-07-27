## 1.对 Vue 数据响应式的理解
Vue实例中的数据发生改变的时候，视图会相应重新渲染，匹配改变后的值，这就是Vue的数据响应式

## 2.这是如何实现的
### 2.1 传入Vue实例的数据，会被遍历所有属性，并且使用 ***Object.defineProperty*** ，设置 ***get*** 和 ***set*** 方法，从而实现了监听和代理
- 关于Object.defineProperty 的 get 和 set 方法
~~~js
let obj={name:"Jack"}
console.log('1.'+obj.name)
Object.defineProperty(obj,"name",
    {
        get(){      
            console.log("get 被触发")
        },
        set(){         
            console.log("set 被触发")
        }
    })
console.log('2.'+obj.name)
obj.name='Rose'
//1.Jack
//get 被触发
//2.undefined
//set 被触发
//get 被触发
//3.undefined
~~~
- obj 在使用 Object.defineProperty 处理后
- 调用obj.name时候，运行get
- 改变obj.name时候，运行set
- 外部不能直接读取到 obj 的 name 的值  

这些 getter/setter 对用户来说是不可见的，但是在内部它们让 Vue 能够追踪依赖，在 property 被访问和修改时通知变更。
### 2.2 每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把“接触”过的数据 property 记录为依赖。
~~~js
let bp={a:0,b:10}
console.log(bp)
new Vue({
  data:bp,
 template:`<div>
 <div class='shot1'>{{a}}</div>  
 <div class='shot2'>{{a}}</div>  
 <div class='shot3'>{{b}}</div> 
 </div>`
}).$mount("#app");
console.log(bp)
~~~
- 使用数据a的依赖 ['.shot1'，'.shot2']
- 使用数据b的依赖 ['.shot3']
 
### 2.3 当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染。

## 3.检测变化时候的注意事项
### 3.1 数据是对象的时候，Vue对于未声明的属性，是无法添加监听和代理的
~~~js
import Vue from "vue";

Vue.config.productionTip = false;

const vm=new Vue({
  data:{a:0},
 template:`<div>
 <div class='shot1'>{{b}}</div>   
 </div>`
}).$mount("#app");
//报错：
//Property or method "b" is not defined on the instance but referenced during render
//b的属性或者方法没有在实例中定义，但是渲染的时候被引用了
~~~
#### 3.1.1 解决方式
- 在data中预先声明
~~~js
    data:{a:0，b:''},
~~~
- 使用Vue.set或者this.$set
~~~js
    Vue.set(this.obj,'b',1) 
    this.$set(this.obj,'b',1)
~~~

### 3.2 数据是数组的时候，不能检测某些变动
- 当你利用索引直接设置一个数组项时
- 当你修改数组的长度时
~~~js
import Vue from "vue/dist/vue.js";

Vue.config.productionTip = false;

new Vue({
  data: {
    array: ["a", "b", "c"]
  },
  template: `
    <div>
      {{array}}
      <button @click="changeArray">change Array</button>
      <button @click="changeLength">change Length</button>
    </div>
  `,
  methods: {
    changeArray() {
      this.array[2] = "d";  
    },
    changeLength() {
      this.array.length = 5;     
    }
  }
}).$mount("#app");
//可以看到一点用都没
~~~
- 解决办法
~~~js
changeArray() {
      Vue.set(this.array,2,'5')
    }
changeLength() {
      this.array.splice(3)     
    }
~~~
在changeLength()例子中我们可以看到，作者把原始数组操作方法进行了改进，这样就能同时给数组元素添加监听和代理
- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()