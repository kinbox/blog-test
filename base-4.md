# 由渲染器原理看CSS动画
## 1. 渲染器原理
1. 根据HTML构建html树（DOM）
2. 根据CSS构建CSS树（CSSOM）
3. 将2颗树合并为一个渲染树（render Tree）
4. Layout 布局（文档流，盒模型，计算大小和位置）
5. Paint 绘制（把边框颜色，文字颜色，阴影效果等画出来）
6. Compose 合成（根据层叠关系展示最终画面）

## 2.CSS动画原理
页面上元素的动画一般是由 JS 或者 *hover* 这样的伪标签来驱动CSS属性而形成的，所以考虑到动画性能就要看是否会以上的渲染步骤造成影响。
### 三种方式
* 全走：CSS>样式>布局>绘制>合成
   * 如 *div.remove()* 会触发当前小时，其他元素重新布局
* 跳过 Layout
   * 如 *改变背景颜色* 直接 重新Paint + Compose
* 跳过 Layout和Paint
   * 如 *改变transform* 只有Compose

Tips：关于CSS属性改变会触发哪些流程可以在 https://csstriggers.com/ 查看。

由于前面提到的原因，在不借助别的库（如GreenSock）的情况下，普遍使用的动画方案就是Transform。

## 3.Transform基本用法
### 3.1 transform常用功能
* 位移 translate
* 缩放 scale
* 旋转 rotate
* 倾斜 skew

Tips
* 一般需要配合Transition
* inline元素不知道transform，需要变成bloc
  
### 3.2 translate
一般用法：
```css
translateX(50px,50px);
translateY(50%,50%)
translate(50%,50%)
``` 
Tips

*translate(-50%,50%)*  常用语绝对定位元素的居中。

### 3.3 scale
一般用法：
```css
scaleX(1.2);
scaleX(50%);
``` 

### 3.4 rotate
一般用法：
```css
rotate(15deg);
rotateX(30deg);
rotateY(45deg);
rotateZ(60deg);
```
  
### 3.5 skew
一般用法：
```css
skewX(15deg);
skewY(30deg);
skewZ(45deg);
``` 
### 3.6 Transform组合
一般用法：
```css
transform:scale(0.3) translate(50%,50%);
``` 
## 4.Transition
过渡 *transition* 用于补充2个变化之间的中间帧
语法是
```css
transition:属性名 时长 过渡方式 延迟
``` 
范例
```css
transition: transform 1s linear 2s
``` 

## 4.Animation
当超过了2个节点的时候就需要animation配合@keyframes
```css
animation:时长丨过渡方式丨延迟丨次数丨方向丨填充模式丨是否暂停丨动画名
``` 
范例
```css
.out {
            animation: jump 1s infinite ease;
        }



@keyframes jump {
            0% {
                transform: none;
            }

            30% {
                transform: scale(1.1);
            }

            100% {
                transform: none;
            }

``` 