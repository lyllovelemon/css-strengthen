# css如何工作-解析和绘制css的关键路径
## 渲染步骤
1.html解析形成DOM树

2.css解析形成css OM

3.DOM和css OM结合形成渲染树

4.生成布局

5.页面绘制

### DOM树阶段
在这个阶段html解析成类似树的数据结构的DOM，DOM包含html页面的所有节点。每个节点
包含html元素的数据(比如attributes、id、class)。如果这个节点下层有html元素，它的子html元素会被
解析成子节点。
![Dom](https://lyllovelemon.github.io/css-strengthen/src/images/md/dom.png )

### css OM 阶段
当浏览器生成DOM树之后，就会开始解析css样式文件，包括内联样式、行内样式和外部样式。
解析过后的css文件会生成css OM(object model)，简称为对象模型。对象模型的构造与树的结构很相像，
如图所示：
 ![om](https://lyllovelemon.github.io/css-strengthen/src/images/md/om.png )

我们解析css文件里所有的选择器，然后把它们展示在树结构里，如果解析的是单个选择器，它会被解析到树的根节点。
网状选择器会被解析到父节点之下，即在父节点下面生成子节点。css解析的顺序是从右到左，以此确保能生成正确的节点。

### 渲染树阶段
浏览器把DOM树和css OM结合，生成渲染树。在此阶段会在DOM树中移除掉不需要的节点，比如不可见元素。不可见元素包括<head>、<script>
和<meta>,以及hidden属性的元素。然后进入到css OM中，识别每个元素分别对应哪个css选择器的样式，当遇到display:none的元素时，会把该元素移除。
当这些步骤执行完，浏览器可以安全的使用渲染树中的元素绘制页面。
> 注意:opacity:0的元素不会被移除
 ![om](https://lyllovelemon.github.io/css-strengthen/src/images/md/tree.png )

### layout布局阶段
形成了一个完整的渲染树后，进入了布局阶段。布局阶段浏览器会判断每个元素展示在什么地方以及
它会占用多少空间。浏览器会考虑margin、padding、width、height、position等属性。每个元素会进行定位

css盒模型就是在这一阶段发挥作用的，但是需要知道，这一阶段并没有把内容绘制在页面上。

### paint绘制阶段
 绘制发生在布局之后，这一阶段完成后，内容才能绘制在页面上。

## 为何需要了解css如何工作
了解css如何工作能帮助你写出更美观的css，并且能够进行性能优化，对css选择器有一个更深层次的理解。

## 参考文章
+ [how css works parsing painting css in the critical rendering path](https://blog.logrocket.com/how-css-works-parsing-painting-css-in-the-critical-rendering-path-b3ee290762d3)