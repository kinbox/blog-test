# JS 函数的执行时机
## 1.容易出错的一段代码
```javascript
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
//输出结果6个6
```
为什么会是6个6，而不是012345呢？

看流程：首先定义了全局的i值为0，然后使用for循环，赋值了i的值为0，添加表达式2：i<6，添加表达式3：i++，循环体为setTimeout(()=>{console.log(i)},0)，表示隔一段时间尽快console.log出i的值。

但是此处i在循环体的作用域内部不存在，只有向上就近查找a的声明，这时候 console.log(i) 和  let i = 0 形成了闭包

所以要先跑完for循环，在 i 经历了012345的变化后。console.log(i)已经堆了6次栈，同时for循环结束i=5又自加了一次i=6，然后开始运算6次堆栈的console.log(i)，结果为6个6。

## 2.代码改写
```javascript
for(let i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
//结果012345
```
在for的()中使用let声明，会创建一个隐藏的作用域
此时console.log(i)在查找i声明时候会发现依旧在for的作用域内，所以每次console出的i值是一直随着循环更新的

## 3.代码再次改写
```javascript
for(var i = 0; i<6; i++){
    let j=i
  setTimeout(()=>{
    console.log(j)
  },0)
}
//结果012345
```
console.log(j) 和 let j=i构成闭包，i的值传给了j，从而打印出012345