# JQuery基本功能
jQuery是目前使用最广泛的javascript函数库。对于网页开发者来说，学会jQuery是必要的。因为它让你了解业界最通用的技术，为将来学习更高级的库打下基础，并且确实可以很轻松地做出许多复杂的效果。
## 1.jQuery 如何获取元素
使用jQuery的第一步，往往就是将一个选择表达式，放进构造函数jQuery()（简写为$），然后得到被选中的元素。
```javascript
$(document) //选择整个文档对象
$('#myId') //选择ID为myId的网页元素
$('div.myClass') // 选择class为myClass的div元素
$('input[name=first]') // 选择name属性等于first的input元素
```
## 2.jQuery 的链式操作
原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同的操作可以一起进行
```javascript
$('div').find('h3').html('Hello');
//找到div元素,选择其中的h3元素，将其内容改为Hello
$('div').find('h3').html('Hello').end().addClass('red')
//end()方法可以返回到‘find('h3')时’的状态，并且添加red样式
```
## 3.jQuery 如何创建元素
把新元素直接传入jQuery的构造函数就行了
```javascript
$('<p>p1</p>')
$('<div class="container">container</div>')
```

## 4.jQuery 如何移动元素
提供l了两种方法，一种是直接移动该元素，另一种是移动其他元素，使得目标元素达到我们想要的位置。
```javascript
//选择#before移动到#after后面
$('#after').insertAfter($('#before'));
//返回#after
$('#before').after($('after'));
//返回#before
```

## 5.jQuery 如何修改元素的属性
jQuery使用重载的设计方式，让一个函数因为参数的不同而同时有取值（getter）和赋值（setter）的功能。如：
```javascript
$('h1').html() //没有参数，代表h1标签的值
$('h1').html(‘The Winner’) //有string参数，表示对h1赋值为 The Winner
```
   注意的是
   ```javascript
   $('h1') 
   表示h1标签形成的数组的所有元素
   如果只想修改第一个,需写成
   $('h1')[0]
  ```