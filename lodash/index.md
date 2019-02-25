# lodash 学习整理

## Array

#####1. _.chunk(array, [size=1])
> 将数组拆分成size 长度的区块。 如果array 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

```js
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

#####2. _.compact(array) ☆
> 去除数组中的falsely成员

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

#####3. _.concat(array, [values])
> 组合新数组,[values] 可以为新数组 或 值

```js
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);
 
console.log(other);
// => [1, 2, 3, [4]]
 
console.log(array);
// => [1]
```

#####4. _.difference(array, [values]) ☆
> 比较出 array 在 [values] 中不同的这数组并已数组形式返回

```js
_.difference([3, 2, 1], [4, 2]);
// => [3, 1]
```

#####5. _.difference(array, [values]) ☆
> 比较出 array 在 [values] 中不同的这数组并已数组形式返回

```js
_.difference([3, 2, 1], [4, 2]);
// => [3, 1]
```

#####6. _.differenceBy(array, [values], [iteratee=_.identity]) ☆☆
> 原理同上，但可添加一个迭代器 用来对比对象。

```js
_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor);
// => [3.1, 1.3]
 
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
```

#####7. _.drop(array, [n=1])
> 去除array前面的n个元素。（n默认值为1。）(此操作新建了一个对象并不是对原数组进行操作)

```js
_.drop([1, 2, 3]);
// => [2, 3]
 
_.drop([1, 2, 3], 2);
// => [3]
 
_.drop([1, 2, 3], 5);
// => []
 
_.drop([1, 2, 3], 0);
// => [1, 2, 3] 
```

#####8. _.drop(array, [n=1])
> 去除array前面的n个元素。（n默认值为1。）

```js
_.drop([1, 2, 3]);
// => [2, 3]
 
_.drop([1, 2, 3], 2);
// => [3]
 
_.drop([1, 2, 3], 5);
// => []
 
_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

#####9. _.fill(array, value, [start=0], [end=array.length])
> 使用 value 值来填充（替换） array，从start位置开始, 到end位置结束（但不包含end位置）。

```js
var array = [1, 2, 3];
 
_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']
 
_.fill(Array(3), 2);
// => [2, 2, 2]
 
_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```


#####10. _.flattenDeep(array)
> 将array递归为一维数组。

```js
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

#####11. _.indexOf(array, value, [fromIndex=0])
> 返回首次 value 在数组array中被找到的 索引值， 如果 fromIndex 为负值，将从数组array尾端索引进行匹配。

```js
_.indexOf([1, 2, 1, 2], 2);
// => 1
 
// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

#####12. _.join(array, [separator=','])
> 将 array 中的所有元素转换为由 separator 分隔的字符串。

```js
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```
#####13. _.last(array)
> 获取array中的最后一个元素。

```js
_.last([1, 2, 3]);
// => 3
```

#####14  _.pull(array, [values])
> 移除数组array中所有和给定值相等的元素

```js
var array = [1, 2, 3, 1, 2, 3];
 
_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```

#####14.2  _.pullAll(array, values)
> 移除数组array中所有和给定值相等的元素

```js
var array = [1, 2, 3, 1, 2, 3];
 
_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```

#####14.3  _.pullAllBy(array, values, [iteratee=_.identity])
> 区别是这个方法接受一个 iteratee（迭代函数） 调用 array 和 values的每个值以产生一个值，通过产生的值进行了比较。

```js
var array = [{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }];
 
_.pullAllBy(array, [{ 'x': 1 }, { 'x': 3 }], 'x');
console.log(array);
// => [{ 'x': 2 }]
```

#####14.4  _.pullAt(array, [indexes])
> 根据索引 indexes，移除array中对应的元素，并返回被移除元素的数组。 

```js
var array = [5, 10, 15, 20];
var evens = _.pullAt(array, 1, 3);
 
console.log(array);
// => [5, 15]
 
console.log(evens);
// => [10, 20]
```

#####15  _.remove(array, [predicate=_.identity])
> 移除数组中predicate（断言）返回为真值的所有元素，并返回移除元素组成的数组。predicate（断言） 会传入3个参数： (value, index, array)。 

```js
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});
 
console.log(array);
// => [1, 3]
 
console.log(evens);
// => [2, 4]
```

#####16  _.reverse(array)
> 移除数组中predicate（断言）返回为真值的所有元素，并返回移除元素组成的数组。predicate（断言） 会传入3个参数： (value, index, array)。 

```js
var array = [1, 2, 3];
 
_.reverse(array);
// => [3, 2, 1]
 
console.log(array);
// => [3, 2, 1]
```

#####17  _.slice(array, [start=0], [end=array.length])
> 裁剪数组array，从 start 位置开始到end结束，但不包括 end 本身的位置。  

```js
var array = [1, 2, 3];
 
_.reverse(array);
// => [3, 2, 1]
 
console.log(array);
// => [3, 2, 1]
```

#####18  _.uniq(array)
> 创建一个去重后的array数组副本。使用了 SameValueZero 做等值比较。只有第一次出现的元素才会被保留。  

```js
_.uniq([2, 1, 2]);
// => [2, 1]
```

#####19  _.unzip(array) _.zip(array)
> 压缩和借压缩  数组  

```js
var zipped = _.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]]
 
_.unzip(zipped);
// => [['fred', 'barney'], [30, 40], [true, false]]
```







