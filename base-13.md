# 浅析 MVC
## 1.MVC是什么
MVC是一种设计模式，把应用分为3个基本部分
- M model 模型
- V view 视图
- C control 控制器  

这个模式最开始是用于后端的，将业务逻辑，数据，界面拆分到各自的模块里面各司其职,当后期需要改进项目时候大大节约了重构的成本
> Model 用于封装原始数据
~~~js
M = {
    data:{},//原始数据
}
~~~
> View 最红呈现的界面
~~~js
V = {
    el:null,//空元素，用于加载和传递
    html:`...`//视图模板
    render(){}//渲染界面
}
~~~
> Control 连接V和M，处理业务逻辑
~~~js
C  = {
    init(){}//初始化
    bindEvents() // 自动的事件绑定
}
~~~

## 2.EventBus
EventBus,顾名思义事件公交车，是事件之前通信的桥梁
### 2.1 EventBus.on()
~~~js
EventBus.on(eventName,callback)  
//监听事件 (eventName) ,执行回调 (callback) 
~~~
### 2.2 EventBus.trigger()
~~~js
EventBus.trigger()(eventName)  
//触发事件 (eventName)
~~~
~~~js
fn1(){
  EventBus.on('m3',fn(){打印出被点击的div})  
}
fn2(){  
  当div被点击，触发事件'm3'
}
~~~
## 3.表驱动编程
使用哈希表，将函数的参数名和调用以string格式存储，然后通过对key和value的string操作，使其获得一一的映射，大大减少了代码的重复和后期维护时候的不便
~~~js
const cos={
  e:{
    'click #add': 'add',
    'click #minus': 'minus',
    'click #mul': 'mul',
    'click #divide': 'divide',
  }
  add(){},
  minus(){},
  mul(){},
  divide(){},
  bindEvents(){
    for (let hey in cos.e){
      const spaceIndex=key.indexOf(' ')
      const event=key.slice(0,spaceIndex)
      const target=key.slice(spaceIndex+1)
      const func=cos[cos.e[key]]
      $('#main').on(event,target,func)
    }
  }
}
~~~

## 4.模块化
将一个复杂的程序依据一定的规则（规范）封装成几个块（文件）并进行组合。 模块的内部数据的实现是私有的，只是向外部暴露一些接口（方法）与外部其他模块通信。这则就是模块化。  
优点就是降低代码偶尔度，减少重复代码，提高了重用度，结构上更加情绪，便于维护