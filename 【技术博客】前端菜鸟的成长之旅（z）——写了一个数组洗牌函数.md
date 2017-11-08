&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天偶然遇到了一个需要打乱数组的需求，JS中没有现成的方法，于是就动手写了一个。不算是一篇"正经"的博客，只是随手记录一下放在这里吧。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;网上流传着一段经典的洗牌代码：
```
var arr = []
for (var i=0; i<100; i++) {
    arr[i] = i
}
arr.sort(function () { return 0.5 - Math.random() })
var str = arr.join()
alert(str)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;代码倒是很简洁，但是是否高效我有点疑问。主要是sort()方法的计算原理，我在网上没有找到，所以对它的`随机性`和`效率`存疑。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;于是我自己写了以下这段，用的都是最简单的方法。除了Math.random()本身就是伪随机外，应该在`随机性`和`效率`两方面都没有什么太大的问题：
```
var arr = [1,2,3,4,5,6,7,8,9]
var len = arr.length

!function () {
	var array = []
	for (var i=0; i<len; i++) {
		var a = Math.floor(Math.random()*arr.length)
		array.push(arr[a])
		arr.splice(a, 1)
	}
	arr = array
}()

console.log(arr)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原理也非常简单：随机获取原数组中的任意元素，将它push进一个新数组，并在原数组中删除这个元素。往复循环，直到原数组中的所有元素都被取出，并添加进新的数组为止。