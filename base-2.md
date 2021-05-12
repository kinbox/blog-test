# HTML常用标签
## a标签
a标签可以通过它的 href 属性创建通向其他网页、文件、同一页面内的位置、电子邮件地址或任何其他 URL 的超链接。
```html
<a href="https://example.com">Website</a>
```

### 属性
* href
* target
* download
* rel=noopener

### 作用
* 跳转外部页面
* 跳转内部锚点
* 跳转到邮箱或者电话等
  
<hr>
  
## img标签
img 标签将一份图像嵌入文档。
```html
<img src="images/2.jpg">
``` 
### 属性
* alt
* height
* width
* src
  
### 事件
* onload
* onerror
  
## 响应式
max-width:100%

<hr>

## table标签
table 标签表示表格数据 — 即通过二维数据表表示的信息
```html
<table>
    <thead>
        <tr>
            <th colspan="2">The table header</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>The table body</td>
            <td>with two columns</td>
        </tr>
    </tbody>
</table>
``` 
### 相关的标签
* table
* thead
* tbody
* tfoot
* tr
* td
* th
  
### 相关的样式
* table-layout
* border-collapse
* border-spacing

<hr>
## 个人感想

还是有很多要记忆的，下次遇见忘记了还是要去查看文档