#### Doctype含义?
* Doctype声明不属于HTML标签,它是一条指令,告诉浏览器编写页面所使用的的HTML或XHTML版本

#### img的alt与title有何异同？ strong与em的异同？
* alt(alt text):为图片加载失败无法正常显示时用来指定替换文字
* title(tool tip):为元素提供额外说明信息,鼠标移入时显示
* strong:粗体强调标签，强调，表示内容的重要性
* em:斜体强调标签，更强烈强调，表示内容的强调点

#### 行内元素和块级元素的具体区别是什么？行内元素的padding和margin可设置吗？
* 块级元素(block)特性：总是独占一行 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制
* 内联元素(inline)特性：和相邻的内联元素在同一行 宽度(width)、高度(height)、上下内边距和上下外边距无效
* 行内块(inline-block): 拥有内在尺寸，可设置高宽，但不会自动换行 如`<input> 、<img> 、<button> 、<texterea> 、<label>`

#### rgba()和opacity的透明效果有什么不同？
* opacity作用于元素，以及元素内的所有内容的透明度，
* rgba()只作用于元素的颜色或其背景色。（设置rgba透明的元素的子元素不会继承透明效果！）

#### display:none与visibility:hidden的区别是什么？
* display: 隐藏对应的元素但不保留该元素原来的空间。
* visibility: 隐藏对应的元素但保留元素原来的空间。

#### 哪些css属性可以继承？
* 可继承：font系列 line-height text-align text-indent color list-style cursor visibility等
* 不可继承：border padding margin width height 

#### link和@import的区别是?
A. Link属于HTML标签,而@import是css提供的
B. 页面被加载时,link会同时被加载,而@import会等到引用的它的css文件加载完再加载
C. Import只在IE以上才能识别,而link是html标签,无兼容性问题
D. Link方式样式的权重高于@import

#### 什么是CSS Hack?
```js
// 1、条件Hack
<!--[if IE]>
  <style>
    .test{color:red;}
  </style>
<![endif]-->
// 2、属性Hack
.test{
  color:#090\9;   /* For IE8+ */
  *color:#f00;    /* For IE7 and earlier */
  _color:#ff0;     /* For IE6 and earlier */
}
// 3、选择符Hack
* html .test{color:#090;}     /* For IE6 and earlier */
* + html .test{color:#ff0;}    /* For IE7 */
```

#### CSS样式的优先级?
* !important > 内联样式 > id > class > 标签  

#### 重排与重绘
* 重绘: 当在页面上修改了一些不需要改变定位的样式的时候(比如background-color),浏览器只会将新的样式重新绘制给元素
* 重排: 当页面上的改变影响了文档内容,结构或者元素定位时,就会发生重排(或称重新布局).
重排通常由以下改变触发:
1)Dom操作(元素增,删,改或者改变元素顺序)
2)内容的改变,包括Form表单中文字的变化
3)计算或改变css属性
4)增加或删除一个样式表
5)浏览器窗口的操作(改变大小,滚动窗口)

#### 