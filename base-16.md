## computed 和 watch 的区别
- computed就是计算属性的意思
- watch就是监听的意思

## computed
- 是计算一个值的，调用的时候不用加括号, 当属性一样用
- 会根据依赖会自动缓存。依赖不变，这个计算出来的值就不会变

## watch
- 一个属性变化了，我们就去执行一个回调函数，它有2个选项：
- immediate   
表示第一次渲染的时候是否要执行这个回调函数  
默认 false 不执行，true 则是执行
- deep  
我们监听这个属性时候是否要看对象内部属性的变化  
默认 false 不会深入，true 为深入监听

## 总结
1. 如果一个数据依赖于其他数据，那么这个数据需设计为 computed
2. 如果需要在某个数据变化时候做一些事情，使用 watch 来监听这个数据变化