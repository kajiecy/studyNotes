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

#####20  _.debounce(func, [wait=0], [options={}])
> 防抖

```js
addCount(){
    console.log("執行了")
    this.count++;
}
_.debounce(this.addCount, 500,{leading:true,trailing:false,maxWait:1000});
// leading 是否在调用之前延迟
// trailing 触发延迟结束后是否调用
// maxWait 最大等待时间
```

#####21  _.delay(func, wait, [args])
> 延迟

```js
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => 一秒后输出 'later'。
```

#####21  _.once(func)
> 创建一个只能调用 func 一次的函数。 重复调用返回第一次调用的结果。 func 调用时， this 绑定到创建的函数，并传入对应参数。
  
```js
var initialize = _.once(createApplication);
initialize();
initialize();
// `initialize` 只能调用 `createApplication` 一次。
```

#####22  _.isEmpty(value)
> 检查 value 是否为一个空对象，集合，映射或者set。 判断的依据是除非是有枚举属性的对象，length 大于 0 的 arguments object, array, string 或类jquery选择器。


#####23  _.random([lower=0], [upper=1], [floating])
> 产生一个包括 lower 与 upper 之间的数。 如果只提供一个参数返回一个0到提供数之间的数。 如果 floating 设为 true，或者 lower 或 upper 是浮点数，结果返回浮点数。 
  
```js
_.random(0, 5);
// => an integer between 0 and 5
 
_.random(5);
// => also an integer between 0 and 5
 
_.random(5, true);
// => a floating-point number between 0 and 5
 
_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

#####24  _.round(number, [precision=0]) 四舍五入   floor（向下取整） ceil （向上取整）
> 根据 precision（精度） 四舍五入 number。 
  
```js
_.round(4.006);
// => 4
 
_.round(4.006, 2);
// => 4.01
 
_.round(4060, -2);
// => 4100
```

#####25  _.truncate([string=''], [options={}])
> 根据 precision（精度） 四舍五入 number。 
  
```js
_.truncate('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'
 
_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'
 
_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': /,? +/
});
// => 'hi-diddly-ho there...'
 
_.truncate('hi-diddly-ho there, neighborino', {
  'omission': ' [...]'
});
// => 'hi-diddly-ho there, neig [...]'
```

#####26  _.unescape([string=''])   _.escape
> _.escape的反向版。 这个方法转换string字符串中的 HTML 实体 &amp;, &lt;, &gt;, &quot;, &#39;, 和 &#96; 为对应的字符。 
  
```js
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

#####27  _.range([start=0], end, [step=1])
> 创建一个包含从 start 到 end，但不包含 end 本身范围数字的数组。 如果 start 是负数，而 end 或 step 没有指定，那么 step 从 -1 为开始。 如果 end 没有指定，start 设置为 0。 如果 end 小于 start ，会创建一个空数组，除非指定了 step。 
```js
_.range(4);
// => [0, 1, 2, 3]
 
_.range(-4);
// => [0, -1, -2, -3]
 
_.range(1, 5);
// => [1, 2, 3, 4]
 
_.range(0, 20, 5);
// => [0, 5, 10, 15]
 
_.range(0, -4, -1);
// => [0, -1, -2, -3]
 
_.range(1, 4, 0);
// => [1, 1, 1]
 
_.range(0);
// => []
```

#####27  _.uniqueId([prefix=''])
> 生成唯一ID。 如果提供了 prefix ，会被添加到ID前缀上。
```js
_.uniqueId('contact_');
// => 'contact_104'
 
_.uniqueId();
// => '105'
```



