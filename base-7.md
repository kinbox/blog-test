# 初识JavaScript
## 语句和表达式
### 表达式
* 1+5表达式的值是6
* add（1,2）表达式的值为函数的返回值
* console.log表达式的值为函数本身
* console.log(5)表达式值为5
  
### 语句
* var i=0 是一个语句

### 两者区别
* 表达式一般都会有值，语句可能有也可能没有
* 语句一般会改变环境（声明，赋值）
* 上面两句并不是绝对
  
## 标识符
### 规则
* 第一个字符，可以是Unicode字母或$或_或中文
* 后面的字符，除了上面说的还可以是数字
### 示例
```javascript

var _=1
var $=2
var ______=3
var 你好='hi'
```

## if else
### 语法
* if(表达式){语句1}else{语句2}
* {}在语句只有一句时候能省略，不过不建议这样做
最推荐的写法
```javascript
if(表达式){
    语句
}
else if(表达式){
    语句
}else{
    语句
}
```

## while
### 语法
* while(表达式){语句}
* 判断表达式的真假
* 表达式为真，执行区块内的语句，执行完再判断表达式的真假
* 表达式为假，执行后面的语句

## for
### 语法糖
for 是 while的方便写法
### 语法
```javascript
for(语句1;表达式2;语句3){
    循环体
}
```
* 先执行语句1
* 判断表达式2
* 如果为真，执行循环体，并且执行语句3
* 如果为假，跳出循环，执行后面的语句
* 经常和break和continue一起使用


## break
指退出当前最近的一个循环
```javascript
for (var i = 0; i < 5; i++) {
  if (i === 3) {
    break;
  }
console.log(i);
}
}
//流程是
i===0 console.log(i) 0 i++
i===1 console.log(i) 1 i++
i===2 console.log(i) 2 i++
i===3 满足i===3 break 退出 i++ 1===4
//结果是
0
1
2
```

## continue
指退出当前满足条件的这次循环，继续完成后面的循环
```javascript
for (var i = 0; i < 5; i++) {
  if (i === 3) {
    continue;
  }
console.log(i);
}
//流程是
i===0 console.log(i) 0 i++
i===1 console.log(i) 1 i++
i===2 console.log(i) 2 i++
i===3 continue 跳过这次 i++
i===4 console.log(i) 4 i++
i===5 不满足条件了 循环停止
//结果是
0
1
2
4
```

## label
label语句可以与break 和 continue 语句联合使用，从而返回代码中特定的位置。这种联合使用的情况多发生在循环嵌套的情况下:
```javascript
var count = 0;
top:
for (var i=0; i < 6; i++) {
     for (var j=0; j < 6; j++) {
        if (i == 3 && j == 3) {
            break top;
        }
        count++; 
    }
}
console.log(count);  
//结果21

```