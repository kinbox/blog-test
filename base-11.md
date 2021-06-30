# DOM事件机制
事件是javascript和HTML交互基础, 任何文档或者浏览器窗口发生的交互, 都要通过绑定事件进行交互;比如鼠标点击事件、敲击键盘事件等。这样的事件行为都是前端DOM事件的组成部分，不同的DOM事件会有不同的触发条件和触发效果。

## 1.捕获与冒泡的来历
事件冒泡和事件捕获分别由微软和网景公司提出，这两个概念都是为了解决页面中事件流（事件发生顺序）的问题。
```javascript
<div id="father">
        <p id="child">点我</p>
    </div>
```
试问，在father层和child层都有绑定事件的时候，执行顺序是如何的?
网景认为father大于child，father优先执行，child之后执行，名词为捕获
微软认为child是文档末端，所以child优先执行，father之后执行，名词为冒泡
然后两者到W3C那边找个说法，W3C给出了折中的解决方式
* 浏览器先走捕获的流程，再走冒泡的流程。犹如一个'U'字形
* 过程中发现有监听函数AddEventListener就调用
* 开发者可以选择用AddEventListener中的第三个参数决定把其放在捕获还是冒泡阶段

## 2.冒泡（默认,或者参数为falsy）
冒泡，先执行child，再执行father
```javascript
<div id="father">
        <p id="child">点我</p>
</div>
<script>
        const f_div = document.getElementById('father');
        const c_div = document.getElementById('child');
        fn1 = (e) => { console.log('你点到爹了') }
        fn2 = (e) => { console.log('你点到儿了') }
        f_div.addEventListener('click', fn1)
        c_div.addEventListener('click', fn2)
</script>
   //你点到儿了
   //你点到爹了
```

## 3.捕获（带参true）
冒泡，先执行child，再执行father
```javascript
<div id="father">
        <p id="child">点我</p>
</div>
<script>
        const f_div = document.getElementById('father');
        const c_div = document.getElementById('child');
        fn1 = (e) => { console.log('你点到爹了') }
        fn2 = (e) => { console.log('你点到儿了') }
        f_div.addEventListener('click', fn1, true)
        c_div.addEventListener('click', fn2, true)
</script>
   //你点到爹了
   //你点到儿了
```
## 4.捕获和冒泡同时存在
```javascript
<div id="grandfather">
        <div id="father">
            <p id="child">点我</p>
        </div>
</div>
<script>
        const f_div = document.getElementById('father');
        const c_div = document.getElementById('child');
        const g_div = document.getElementById('grandfather');
        f_div.addEventListener('click', () => { console.log('father冒泡') })
        f_div.addEventListener('click', () => { console.log('father捕获') }, true)
        c_div.addEventListener('click', () => { console.log('child冒泡') })
        c_div.addEventListener('click', () => { console.log('child捕获') }, true)
        g_div.addEventListener('click', () => { console.log('grandfather冒泡') })
        g_div.addEventListener('click', () => { console.log('grandfather捕获') }, true)
</script>
   //grandfather捕获
   //father捕获
   //child捕获
   //child冒泡
   //father冒泡
   //grandfather冒泡
```

