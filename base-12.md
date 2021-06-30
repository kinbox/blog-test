# DOM事件委托
事件委托指的是把A(一个或者一组元素)的事件委托到它上级B(father或者grandfather或者grandfather’s father等)层上，当事件在A触发的时候能通过冒泡机制，让B来处理

## 1.事件委托的优势
* ### 省内存
 ```javascript
  <ul id="list">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
  ......
  <li>item n</li>
</ul>
```
假设有一个列表，列表之中有大量的列表项，我们需要在点击每个列表项的时候响应一个事件，常规方式，每个li都需要绑定一个函数，对内存消耗很大，如果使用代理，在ul上函数，li在响应时候就会冒泡到ul处理

* ### 更少的代码
  动态添加或者删除元素时，无需添加/移除处理程序。
  
## 2.事件委托实例
```javascript
<ul id="vod">
  <li id="1">aaa</li>
  <li id="2">bbb</li>
  <li id="3">ccc</li>
</ul>
```
要求点击列表项console出id和对应的表值
### 不使用委托
```javascript
const n = document.getElementsByTagName('li')
for (let i = 0; i < n.length; i++) {
            n[i].addEventListener('click', (e) => {
                console.log(e.target.id + ':' + e.target.innerText)
            })
        }
```
### 使用委托
```javascript
const v = document.getElementById('vod')
fn = (e) => {
            if (e.target.nodeName.toLowerCase() === 'li') {
                console.log(e.target.id + ':' + e.target.innerText)
            }
        }
v.addEventListener('click', fn)
```
上述代码是通过判断 target 下的 id 属性，执行不同的事件
