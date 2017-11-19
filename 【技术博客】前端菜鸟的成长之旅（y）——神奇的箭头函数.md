&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这周其实已经写过一篇博客了，所以今天就来写个短篇的好了~正好一直想写JS的这个神奇的功能——箭头函数。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;之所以说它神奇，是因为它的写法：
```
x => x * x
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这居然是一个函数(= =!)，其效果相当于：
```
function (x) {
    return x * x
}
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这本身就已经足够神奇了吧...<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;箭头函数是ES6新增的一种函数写法，原名叫作 Arrow Function。它相当于一个匿名函数，并且简化了函数的定义。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;箭头函数有两种格式。一种像上面这样，只包含一个表达式，连{ }和 return 都省略掉了。另一种可以包含多条语句，这时候就不能省略{ }和 return 了，写法如下：
```
x => {
    if (x > 0) {
        return x * x
    }else {
        return - x * x
    }
}
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果参数不只一个，就需要用括号()括起来：
```
//两个参数：
(x, y) => x * x + y * y

//没有参数：
() => 3.14

//可变参数:
(x, y, ...rest) => {
    var i, sum = x + y
    for (i=0; i<rest.length; i++) {
        sum += rest[i]
    }
    return sum
}
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当我们需要函数返回一个对象时，需要注意：
```
//以下写法会报错，因为和函数体的{ }有语法冲突
x => { foo: x }

//正确写法：
x => ({ foo: x })
```