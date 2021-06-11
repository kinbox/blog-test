# JS 对象基本用法
## JS 对象的两种声明方式
```javascript
var obj1={a:1,b:2}
var obj2=new Object({a:3,b:4})
```
第二种是标准写法，但是第一种更为简略。

## 删除对象属性
```javascript
delete obj1.a//或者下面
delete obj1['a']
/**结果**/
obj1={b:2}
```

## 查看对象的属性
### 查看自身所有属性名
```javascript
Object.keys(obj1)
/**结果**/
["a", "b"]
```
### 查看自身所有属性值
```javascript
Object.values(obj1)
/**结果**/
[1, 2]
```
### 查看自身所有属性名和属性值
```javascript
Object.values(obj1)
/**结果**/
0:['a',1]
1:['b',2]
```

### 查看自身+公用属性
```javascript
console.dir(obj1)
```

### 查看单独的属性
```javascript
obj['a']//或者下面
obj.a
```
优先使用上面的，下面的点语法需要熟练后再用

## 修改或者增加对象的属性
增同改这里差不多意思。

已有属性则是改，没有属性就是增加。
以下主要讲改属性
### 改属性
* 改自身
```javascript
obj1['a']=10
```

* 批量改自身
```javascript
Object.assign(obj1,{c:3,d:4}
```

* 改共有属性1
```javascript
obj.__proto__['toString']='not commanded'
```

* 改共有属性2
```javascript
Object.prototype['toString']='not commanded'
```

* 改原型1
```javascript
obj1.__proto__=common
```

* 改原型1
```javascript
let obj1=Object.create(common)
```

以上使用了__proto__的[改共有属性1]和[改原型1]的方式强烈不推荐使用。

## 'name' in obj和obj.hasOwnProperty('name') 的区别
```javascript
var obj={name:'ak',age:18}
'name' in obj
//true
obj.hasOwnProperty('name')
//true
```
以上2个结果都是真的，因为obj本来就包含了name的属性
```javascript
var common={name:'ak'}
var obj=Object.create(common)
obj.age=18
'name' in obj
//true
obj.hasOwnProperty('name')
//false
```
以上in是真，因为是其隐藏属性，而hasOwnProperty是假，因为不是其本身的属性，是隐藏属性。