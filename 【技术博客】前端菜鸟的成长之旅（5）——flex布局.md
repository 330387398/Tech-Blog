&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;周三了~继续博客。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这几天被打击到了..感觉自己的技术简直菜得不行了，不行到对人生产生了怀疑..于是决定短期内不按周更了，尽量2天一更吧，把自己能想到的知识点挨个总结写出来，一定一定要努力提升技术水平！！<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天想写的是 flex 布局。在 CSS 3 以前，布局基本上都是 float、position定位之类的方法。——直到 flex 的出现，让一些布局瞬间变得简单了。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;先来看看 flex 能干什么。首先，flex 布局的前提是必须有一个父容器，里面装着若干个子元素（废话...）。在这个前提下，才能实现各种方便快捷的布局功能。代码一：
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>test</title>
  <style>
    .div1 .parent {
      display: flex;
      height: 200px;
      border: 1px solid red;
    }
    .div1 .child {
      width: 100px;
      height: 100px;
      border: 1px solid black;
    }
  </style>
</head>
<body>
  <div class="div1">
    <div class="parent">
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
    </div>
  </div>
</body>
</html>
```
![](https://i.loli.net/2017/11/22/5a1556a0ee4ba.png)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最基本也是最核心的功能：让块级元素水平排列。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;接下来，为 .child 添加样式 margin: auto;
![](https://i.loli.net/2017/11/22/5a15573ac6dca.png)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;神奇地水平居中了。——这只是刚刚开始。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;代码二：
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>test</title>
  <style>
    .div2 .parent {
      display: flex;
      border: 3px solid red;
    }
    .div2 .child {
      flex: 1;
      height: 100px;
      border: 1px solid;
    }
  </style>
</head>
<body>
  <div class="div2">
    <div class="parent">
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
    </div>
  </div>
</body>
</html>
```
![](https://i.loli.net/2017/11/22/5a1558a7dcf61.png)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;flex: 1; 样式使得子元素均匀、无缝隙地水平排列在父容器中。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;同样的，我们做一点小小的改动：为 .child:first-child 第一个子元素添加样式 flex: 2;
![](https://i.loli.net/2017/11/22/5a15597302f6d.png)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;第一个子元素变宽了。仔细观察不难发现，它的宽度正好是其它子元素的两倍。也就是说 flex 属性设定的值，是几个子元素排列时所占的比例。在这个例子中，它们的比例就是2：1：1。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;接着来。代码三：
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>test</title>
  <style>
    .div3 .parent {
      display: flex;
      align-items: center;
      border: 3px solid red;
    }
    .div3 .child:first-child {
      margin-right: 10px;
      width: 50px;
      height: 50px;
      border: 1px solid;
    }
    .div3 .child:nth-child(2) {
      flex:1;
      height: 150px;
      border: 1px solid;
    }
  </style>
</head>
<body>
  <div class="div3">
    <div class="parent">
      <div class="child"></div>
      <div class="child"></div>
    </div>
  </div>
</body>
</html>
```
![](https://i.loli.net/2017/11/22/5a1560cb65e73.png)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这段代码当中，flex 体现了两个功能：align-items: center; 垂直居中，以及 flex: 1; 让右侧的子元素占满了整个剩余空间。这里的 flex 值是几其实都无所谓，关键在于，左侧子元素宽度确定了之后，右侧子元素的 flex 属性让它占满了整个剩余的空间。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;接着来。代码四：
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>test</title>
  <style>
    .div4 .parent {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      width: 600px;
      border: 3px solid red;
    }
    .div4 .child {
      margin: 10px 0;
      width: 100px;
      height: 100px;
      border: 1px solid;
      border-radius: 50px;
    }
  </style>
</head>
<body>
  <div class="div4">
    <div class="parent">
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div>
    </div>
  </div>
</body>
</html>
```
![](https://i.loli.net/2017/11/22/5a1563473a3e0.png)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这段代码的关键在于：flex-wrap: wrap; 这个样式让子元素排列不下的时候自动换行；justify-content: space-between; 这个样式让子元素平均排列，并且两边不留空隙。<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;说了这么多，实在是有点晕了：flex 各种样式属性太多太杂了，功能也十分的强大。到底用的时候要怎么办呢？其实我们只需要记住一些常见的用法。对于一些不常用的布局方式，需要使用的时候只要在官方文档稍微找一下，很快就能找到需要的布局方式和代码啦~<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; https://css-tricks.com/snippets/css/a-guide-to-flexbox/<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最后还有一点，flex 有一个很大的局限性：由于它是CSS 3的新增样式，也导致了它在PC端兼容性比较差，一般情况下用在移动端的情况较为广泛。