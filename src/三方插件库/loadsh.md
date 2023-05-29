# 一. loadsh 是js使用数据操作库 ，实用性极高，必看

1. <script src="lodash.js"></script>

2. npm i --save lodash



# 二. 引入版本 3.0.0

将数组（array）拆分成多个 size 长度的区块，并将这些区块组成一个新数组。 如果array 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

_.chunk(array, [size=1])

array (Array): 需要处理的数组

[size=1] (number): 每个数组区块的长度

(Array): 返回一个包含拆分区块的新数组（注：相当于一个二维数组）。

_.chunk(['a', 'b', 'c', 'd'], 2);  2表示：拆分为2维数组
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);  3表示：将前3个拆分为1个数组，将剩余的为另一个数组
// => [['a', 'b', 'c'], ['d']]



# 三.引入版本 0.1.0

_.compact(array)

创建一个新数组，包含原数组中所有的非假值元素。例如false, null,0, "", undefined, 和 NaN 都是被认为是“假值”。

_.compact(array)

(Array): 返回过滤掉假值的新数组。
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]



# 四.引入版本 4.0.0

_.concat(array, [values])

创建一个新数组，将array与任何数组 或 值连接在一起。


array (Array): 被连接的数组。
[values] (...*): 连接的值。

var array = [1];
var other = _.concat(array, 2, [3], [[4]]);
 
console.log(other);
// => [1, 2, 3, [4]]
 
console.log(array);
// => [1]



# 五.引入版本 0.1.0

_.difference(array, [values])

创建一个具有唯一array值的数组，每个值不包含在其他给定的数组中。（注：即创建一个新数组，这个数组中的值，为第一个数字（array 参数）排除了给定数组中的值。）该方法使用SameValueZero做相等比较。结果值的顺序是由第一个数组中的顺序确定。

array (Array): 要检查的数组。
[values] (...Array): 排除的值。

(Array): 返回一个过滤值后的新数组。

_.difference([3, 2, 1], [4, 2]);
// => [3, 1]




# 六.引入版本 4.0.0_

_.differenceBy(array, [values], [iteratee=_.identity])

这个方法类似_.difference ，除了它接受一个 iteratee （注：迭代器）， 调用array 和 values 中的每个元素以产生比较的标准。 结果值是从第一数组中选择。iteratee 会调用一个参数：(value)。（注：首先使用迭代器分别迭代array 和 values中的每个元素，返回的值作为比较值）。

array (Array): 要检查的数组。
[values] (...Array): 排除的值。
[iteratee=_.identity] (Array|Function|Object|string): iteratee 调用每个元素。


_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor);
// => [3.1, 1.3]
<!-- 从第一数组中选择最小和最大的值 -->
 
// The `_.property` iteratee shorthand.
_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]
<!-- 从第一数组中选择不重复的值 -->



# 七.引入版本 4.0.0_

_.differenceWith(array, [values], [comparator])

这个方法类似_.difference ，除了它接受一个 comparator （注：比较器），它调用比较array，values中的元素。 结果值是从第一数组中选择。comparator 调用参数有两个：(arrVal, othVal)。

array (Array): 要检查的数组。
[values] (...Array): 排除的值。
[comparator] (Function): comparator 调用每个元素。

(Array): 返回一个过滤值后的新数组。

var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
 
_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]
<!-- 从第一objects的数组中，选择不重复的值 -->



# 八.引入版本 0.5.0

_.drop(array, [n=1])

创建一个切片数组，去除array前面的n个元素。（n默认值为1。）

array (Array): 要查询的数组。
[n=1] (number): 要去除的元素个数。

_.drop([1, 2, 3]); n默认值为1
// => [2, 3]
 
_.drop([1, 2, 3], 2);
// => [3]
 
_.drop([1, 2, 3], 5);
// => []
 
_.drop([1, 2, 3], 0);
// => [1, 2, 3]




# 九.引入版本 3.0.0

_.dropRight(array, [n=1])

创建一个切片数组，去除array尾部的n个元素。（n默认值为1。）

array (Array): 要查询的数组。
[n=1] (number): 要去除的元素个数。

(Array): 返回array剩余切片。

_.dropRight([1, 2, 3]);n默认值为1。
// => [1, 2]
 
_.dropRight([1, 2, 3], 2);
// => [1]
 
_.dropRight([1, 2, 3], 5);
// => []
 
_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]




# 十.引入版本 3.0.0

_.dropRightWhile(array, [predicate=_.identity])

创建一个切片数组，去除array中从 predicate 返回假值开始到尾部的部分。predicate 会传入3个参数： (value, index, array)。

array (Array): 要查询的数组。
[predicate=_.identity] (Function): 这个函数会在每一次迭代调用。
返回值

(Array): 返回array剩余切片。

var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];
 
_.dropRightWhile(users, function(o) { return !o.active; });
// => objects for ['barney']
 
// The `_.matches` iteratee shorthand.
_.dropRightWhile(users, { 'user': 'pebbles', 'active': false });
// => objects for ['barney', 'fred']
 
// The `_.matchesProperty` iteratee shorthand.
_.dropRightWhile(users, ['active', false]);
// => objects for ['barney']
 
// The `_.property` iteratee shorthand.
_.dropRightWhile(users, 'active');
// => objects for ['barney', 'fred', 'pebbles']



# 十一.引入版本 3.0.0

_.dropWhile(array, [predicate=_.identity])

创建一个切片数组，去除array中从起点开始到 predicate 返回假值结束部分。predicate 会传入3个参数： (value, index, array)。

array (Array): 要查询的数组。
[predicate=_.identity] (Function): 这个函数会在每一次迭代调用。


(Array): 返回array剩余切片。

 
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];
 
_.dropWhile(users, function(o) { return !o.active; });
// => objects for ['pebbles']
 
// The `_.matches` iteratee shorthand.
_.dropWhile(users, { 'user': 'barney', 'active': false });
// => objects for ['fred', 'pebbles']
 
// The `_.matchesProperty` iteratee shorthand.
_.dropWhile(users, ['active', false]);
// => objects for ['pebbles']
 
// The `_.property` iteratee shorthand.
_.dropWhile(users, 'active');
// => objects for ['barney', 'fred', 'pebbles']




# 十二.引入版本 3.2.0

_.fill(array, value, [start=0], [end=array.length])

使用 value 值来填充（替换） array，从start位置开始, 到end位置结束（但不包含end位置）。

Note: 这个方法会改变 array（注：不是创建新数组）。

array (Array): 要查询的数组。
[predicate=_.identity] (Function): 这个函数会在每一次迭代调用。
返回值

array (Array): 要填充改变的数组。
value (*): 填充给 array 的值。
[start=0] (number): 开始位置（默认0）。
[end=array.length] (number):结束位置（默认array.length）。

(Array): 返回 array。

var array = [1, 2, 3];
 
_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']
<!-- a为替换的值 -->
 
_.fill(Array(3), 2);
// => [2, 2, 2]
<!-- 共有3项，都替换为2 -->
 
_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
<!-- 想不通 -->




# 十三.引入版本 1.1.0

_.findIndex(array, [predicate=_.identity], [fromIndex=0])

该方法类似_.find，区别是该方法返回第一个通过 predicate 判断为真值的元素的索引值（index），而不是元素本身。

(number): 返回找到元素的 索引值（index），否则返回 -1。

var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];
 
_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
 
// The `_.matches` iteratee shorthand.
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1
 
// The `_.matchesProperty` iteratee shorthand.
_.findIndex(users, ['active', false]);
// => 0
 
// The `_.property` iteratee shorthand.
_.findIndex(users, 'active');
// => 2





# 十四.引入版本2.0.0

_.findLastIndex(array, [predicate=_.identity], [fromIndex=array.length-1])

这个方式类似_.findIndex， 区别是它是从右到左的迭代集合array中的元素。

array (Array): 要搜索的数组。
[predicate=_.identity] (Array|Function|Object|string): 这个函数会在每一次迭代调用。
[fromIndex=array.length-1] (number): The index to search from.

var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];
 
_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
 
// The `_.matches` iteratee shorthand.
_.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0
 
// The `_.matchesProperty` iteratee shorthand.
_.findLastIndex(users, ['active', false]);
// => 2
 
// The `_.property` iteratee shorthand.
_.findLastIndex(users, 'active');
// => 0




# 十五.引入版本1.0.0

_.head(array)

获取数组 array 的第一个元素。

_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined


# 十六.引入版本0.1.0

_.flatten(array)

减少一级array嵌套深度。

array (Array): 需要减少嵌套层级的数组。
 
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]




# 十七.引入版本3.0.0

_.flattenDeep(array)

将array递归为一维数组。

(Array): 返回一个的新一维数组。
 
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]



# 十八.引入版本4.4.0

_.flattenDepth(array, [depth=1])

根据 depth 递归减少 array 的嵌套层级

array (Array): 需要减少嵌套层级的数组。
[depth=1] (number):最多减少的嵌套层级数。
 
var array = [1, [2, [3, [4]], 5]];
 
_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]
 
_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]



# 十九.引入版本4.0.0

_.fromPairs(pairs)

与_.toPairs正好相反；这个方法返回一个由键值对pairs构成的对象。

pairs (Array): 键值对pairs。
 
_.fromPairs([['fred', 30], ['barney', 40]]);
// => { 'fred': 30, 'barney': 40 }



# 二十.引入版本0.1.0

_.head(array)

array (Array): 要查询的数组。

(*): 返回数组 array的第一个元素。
 
_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined




# 二十一.引入版本0.1.0

_.indexOf(array, value, [fromIndex=0])

使用SameValueZero 等值比较，返回首次 value 在数组array中被找到的 索引值， 如果 fromIndex 为负值，将从数组array尾端索引进行匹配。

array (Array): 需要查找的数组。
value (*): 需要查找的值。
[fromIndex=0] (number): 开始查询的位置。
 
_.indexOf([1, 2, 1, 2], 2);
// => 1
 
// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
