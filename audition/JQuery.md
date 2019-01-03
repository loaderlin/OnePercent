### JQuery库中的$()是什么

$()函数是JQuery函数的别称

$()函数用于将任何对象包裹成JQuery对象，接着就可以被允许调用定义在JQuery对象上的多个不同方法。

JQuery支持不同类型的选择器，有ID选择器，Class选择器，标签选择器

### $(document).ready() 函数是什么，干什么用的？和JavaScript中的window.onload()事件的异同？

ready() 函数用于在文档进入ready状态时执行代码。当DOM完全加载（HTML被完全解析DOM树构建完成时），JQuery允许我们的执行代码。

window.onload()事件需要等待DOM被创建，还要等待包括 大型图片、音频、视频等所有的外部资源全部都加载完全，才能执行；

```js
JQuery.noConflict() //将变量$的控制权让渡
var $j = JQuery.noConflict(); //自定义一个比较短快捷方式
```

### 基本类型选择器

1. 元素选择器
2. 类选择器
3. id选择器
4. 通配符选择器 * 
5. 属性选择器

### 结合选择器

1. 相邻兄弟选择器 div + p 【表示p元素为选择项，但是他的前方紧邻的兄弟必须是div】
2. 通用相邻元素 div ~ p 【表示p元素为选择项，但是他的前方必须有div兄弟元素，可以不紧邻】
3. 子选择器 div > p 【表示p元素的直接父级元素必须是div才会匹配】
4. 后代选择器 div p 【空格即可，所少个空格无关】
5. 自身选择器 div.test 【有class为test的div元素】

### 伪类选择器

```js
:active  [当用鼠标交互时，它代表的是用户按下按键和松开按键之间的时间。 :active 伪类通常用来匹配tab键交互]

:checked  [一些选择表单元素被选择了，可以用于实现点击某些CheckBox来线上更多的模块]

:hover [适用于用户使用指示设备虚指一个元素（没有激活它）的情况，大部分是指鼠标悬停]

:link [链接]

:visited [被访问过的链接]
```

**注意链接的匹配：需要遵循LVHA的先后顺序，即：:link — :visited — :hover — :active。**

### 伪元素选择器

伪元素可以看做元素一样处理，大部分都还没标准化，用的较多的也就是::before ::after

```js
::after (:after)
::before (:before)
```

### JQuery 选择器

```js
:first    $("p:first")    第一个 <p> 元素
:last    $("p:last")    最后一个 <p> 元素
:even    $("tr:even")    所有偶数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。
:odd    $("tr:odd")    所有奇数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。
:eq(index)    $("ul li:eq(3)")    列表中的第四个元素（index 值从 0 开始）
:gt(no)    $("ul li:gt(3)")    列举 index 大于 3 的元素
:lt(no) $("ul li:lt(3)")    列举 index 小于 3 的元素
:header    $(":header")    所有标题元素 <h1>, <h2> ...
:animated    $(":animated")    所有动画元素
:contains(text)    $(":contains('Hello')")    所有包含文本 "Hello" 的元素
:has(selector)    $("div:has(p)")    所有包含有 <p> 元素在其内的 <div> 元素
:hidden    $("p:hidden")    所有隐藏的 <p> 元素
:visible    $("table:visible")    所有可见的表格
[attribute$=value]    $("[href$='.jpg']")    所有带有 href 属性且值以 ".jpg" 结尾的元素
:input    $(":input")    所有 input 元素
:text    $(":text")    所有带有 type="text" 的 input 元素
:password    $(":password")    所有带有 type="password" 的 input 元素
:radio    $(":radio")    所有带有 type="radio" 的 input 元素
:checkbox    $(":checkbox")    所有带有 type="checkbox" 的 input 元素
:submit    $(":submit")    所有带有 type="submit" 的 input 元素
:reset    $(":reset")    所有带有 type="reset" 的 input 元素
:button    $(":button")    所有带有 type="button" 的 input 元素
:image    $(":image")    所有带有 type="image" 的 input 元素
:file    $(":file")    所有带有 type="file" 的 input 元素
```