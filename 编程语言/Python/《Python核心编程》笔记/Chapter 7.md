# Chapter 7 {#chapter_7}

## 字典

字典是Python语言中唯一的映射类型。映射类型对象中的键(通过哈希值进行索引) 和指向的对象(值)是一对一的关系。一个字典对象是可变的，它是一个容器类型，能存储任意个数的 Python 对象，其中也包括其他容器类型。

字典类型和序列类型容器类(列表、元组)的区别是存储和访问数据的方式不同。

* 序列类型只用数字类型的键(从序列的开始起按数值顺序索引)。
* 映射类型可以用其他对象类型做键； 一般最常见的是用字符串做键(keys)。和序列类型的键不同，映射类型的键(keys)直接，或间接地和存储的数据值相关联。但因为在映射类型中，我们不再用"序列化排序"的键(keys),所以映射类型中的数据是无序排列的。

一个字典项的语法格式如下，而且，多条字典条目被包含在({}) 里。

~~~

 >>> {key1 : value, key2 : value, ...}
 >>> dic = {}	#创建一个空字典

~~~

从 Python 2.2 版本起，可以用工厂方法 dict() 来创建字典。

~~~

 >>> dic = dict([[key, value], [key, value]])

~~~

从 Python 2.3 版本起, 可以用一个很方便的内建方法 fromkeys() 来创建一个"默认"字典, 字典中元素具有相同的值 (如果没有给出， 默认为 None)。

访问字典元素的值：

~~~

 >>> dic[key]

~~~

遍历字典元素的值：

~~~

for key in dict.keys(): 
	print 'key=%s, value=%s' % (key, dict2[key]) 

~~~

从Python2.2开始，可以不必再用keys()方法获取供循环使用的键值列表了。 可以用迭代器来轻松地访问类序列对象(sequence-like objects)，比如字典和文件。只需要用字典的名字就可以在 for 循环里遍历字典。

~~~

 >>> for key in dic:
	print dic[key]

~~~


更新字典：

~~~

 >>> dic[key] = value

~~~

如果key是已经存在在dic中的，则key对应的值被修改为value，如果key不存在dic中，则引入一个新的key:value字典项。

删除字典元素和字典

~~~

del dict2['name']	#删除键为"name"的条目  
dict2.clear()		#删除 dict2 中所有的条目 
del dict2		#删除整个 dict2 字典 
dict2.pop('name')	#删除并返回键为“name”的条目 

~~~

### 映射类型操作符

#### 字典的下标操作符

下标操作符是唯一仅用于字典类型的操作符，它和序列类型里单一元素的切片(slice)操作符很相象。字典类型是用键(key)查询字典中的元素。

下标操作符既可以用于给字典赋值，也可以用于从字典中取值

#### 成员关系操作(in,not in)

从Python2.2起可以使用成员关系操作符判断一个元素是否属于一个容器元素。

### 映射类型的内建函数和工厂函数

#### cmp()

字典是通过这样的算法来比较的:首先是字典的大小，然后是键，最后是值。

* 比较字典长度，如果字典的长度不同，那么用 cmp(dict1, dict2) 比较大小时，如果字典 dict1 比 dict2 长，cmp()返回正值，如果 dict2 比 dict1 长，则返回负值。

* 比较字典的键，如果两个字典的长度相同，那就按字典的键比较；键比较的顺序和 keys()方法返回键的顺序相同。(注意: 相同的键会映射到哈希表的同一位置，这保证了对字典键的检查的一致性。) 这时，如果两个字典的键不匹配时，对这两个(不匹配的键)直接进行比较。当 dict1 中第一个不同的键大于dict2中第一个不同的键，cmp()会返回正值。

* 比较字典的值，如果两个字典的长度相同而且它们的键也完全匹配，则用字典中每个相同的键所对应的值进行比较。一旦出现不匹配的值，就对这两个值进行直接比较。若 dict1 比 dict2 中相同的键所对应的值大，cmp()会返回正值。


### 映射类型相关的函数

#### dict()

工厂函数被用来创建字典。如果不提供参数，会生成空字典。

当容器类型对象作为一个参数传递给方法 dict()时，如果参数是可以迭代的，即一个序列，或是一个迭代器，或是一个支持迭代的对象，那每个可迭代的元素必须成对出现。在每个值对中，第一个元素是字典的键、第二个元素是字典中的值。

如果输入参数是(另)一个映射对象，比如，一个字典对象，对其调用 dict()会从存在的字典里复制内容来生成新的字典。新生成的字典是原来字典对象的浅复制版本，它与用字典的内建方法 copy() 生成的字典对象是一样的。但是从已存在的字典生成新的字典速度比用 copy()方法慢。

从 Python 2.3 开始，调用 dict()方法可以接受字典或关键字参数字典

#### len() 

内建函数len()很灵活。它可用在序列、映射类型和集合上。对字典调用len()，它会返回所有元素(键-值对)的数目

#### hash()

内建函数 hash()本身并不是为字典设计的方法，但它可以判断某个对象是否可以做一个字典的键。将一个对象作为参数传递给 hash(), 会返回这个对象的哈希值。 只有这个对象是可哈希的，才可作为字典的键 (hash函数的返回值是整数)。

如果用比较操作符来比较两个数值，发现它们是相等的，那么即使二者的数据类型不同，它们也会得到相同的哈希值。

如果非可哈希类型作为参数传递给 hash()方法，会产生 TypeError 错误。

### 字典的键

不允许一个键对应多个值,必须明确一条原则：每个键只能对应一个项。也就是说，一键对应多个值是不允许的。 当有键发生冲突(即，字典键重复赋值)，取最后(最近)的赋值。
Python 并不会因字典中的键存在冲突而产生一个错误，它不会检查键的冲突是因为，如果真这样做的话，在每个键-值对赋值的时候都会做检查，这将会占用一定量的内存。

键必须是可哈希的，大多数 Python 对象可以作为键；但它们必须是可哈希的对象。像列表和字典这样的可变类型，由于它们不是可哈希的，所以不能作为键。所有不可变的类型都是可哈希的，因此它们都可以做为字典的键。一个要说明的是问题是数字：值相等的数字表示相同的键。换句话来说，整型数字1和浮点数1.0的哈希值是相同的，即它们是相同的键。

同时，也有一些可变对象(很少)是可哈希的，它们可以做字典的键，但很少见。举一个例子，一个实现了\_\_hash\_\_() 特殊方法的类。因为 \_\_hash\_\_()方法返回一个整数，所以仍然是用不可变的值(做字典的键)。

用元组做有效的键，必须要加限制：元组中只包括像数字和字符串这样的不可变参数，才可以作为字典中有效的键。 

## 集合类型

集合对象是一组无序排列的可哈希的值，集合成员可以做字典中的键。

集合(sets)有两种不同的类型：

* 可变集合 (set)
* 不可变集合(frozenset)
    
注意:可变集合(set)不是可哈希的，因此既不能用做字典的键也不能做其他集合中的元素

集合由Python 2.3引入，通过集合(sets)模块来创建，并通过ImmutableSet类和Set类进行访问。在Python 2.4中，这些类被C重写后包含到Python中。

### 创建集合类型

集合类型只能由集合的工厂函数set()和frozenset()创建。

~~~

 >>> set([1, 2, 3])
 set([1, 2, 3])

~~~

### 访问集合中的值

通过成员操作符(in /not in)测试一个元素是否是集合中的值。

### 集合类型操作符

#### 标准类型操作符(适用所有的集合类型)

##### 成员关系 (in, not in)

Python 中的 in 和 not in 操作符决定某个元素是否是一个集合中的成员。

##### 集合等价/不等价(== / !=)

等价/不等价被用于在相同或不同的集合之间做比较。两个集合相等是指，对每个集合而言，当且仅当其中一个集合中的每个成员同时也是另一个集合中的成员（对比的是hash值）。
集合等价/不等价与集合的类型或集合成员的顺序无关，只与集合的元素有关。

##### 子集/超集(<,<= / >,>=)

set用Python的比较操作符检查某集合是否是其他集合的超集或子集。"小于"符号(<, <=)用来判断子集，"大于"符号(>, >=)用来判断超集。

~~~

 >>> set1 = set([1, 2, 3])
 >>> set2 = set([2, 3])

 >>> set2 < set1
 True

 >>> set2 <= set1
 True

 >>> set1 > set2
 True

 >>> set1 >= set2
 True

~~~

#### 集合类型操作符(适用所有的集合类型)

联合( | ) 

联合(union)操作和集合的OR操作是等价的，联合符号有一个等价的方法:union()。

~~~

 >>> set1 = set([1, 2, 3])
 >>> set2 = set([2, 3])
 >>> set3 = set([4, 5, 6])
 >>> set1 | set3
 set([1, 2, 3, 4, 5, 6])

~~~

交集( & ) 

你可以把交集操作比做集合的AND操作，交集符号有一个等价的方法:intersection()。

~~~

 >>> set1 = set([1, 2, 3])
 >>> set2 = set([2, 3])
 >>> set1 & set2
 set([2, 3])

~~~

差补/相对补集( –) 

两个集合(s 和 t)的差补或相对补集是指一个集合 C，该集合中的元素，只属于集合 s，而不属于集合 t。差符号有一个等价的方法，difference()。

~~~

 >>> set1 = set([1, 2, 3])
 >>> set2 = set([2, 3])
 >>> set1 - set2
 set([1])

~~~

对称差分( ^ ) 

和其他的布尔集合操作相似，对称差分是集合的 XOR(又称"异或"(exclusive disjunction)).两个集合(s 和 t)的对称差分是指另外一个集合 C,该集合中的元素，只能是属于集合s或者集合t的成员，不能同时属于两个集合。对称差分有一个等价的方法，symmetric_difference()。

~~~

 >>> set2 ^ set3
 set([2, 3, 4, 5, 6])

 >>> set1 ^ set2
 set([1])

~~~

#### 混合集合类型操作

如果左右两个操作数的类型相同，既都是可变集合或不可变集合, 则所产生的结果类型是相同的，但如果左右两个操作数的类型不相同(左操作数是 set，右操作数是 frozenset，或相反情况)，则所产生的结果类型与左操作数的类型相同。

~~~

 >>> set1 = set([1, 2])
 >>> set2 = frozenset([1, 2])
 >>> type(set1 | set2)
 <type 'set'>

 >>> type(set2 | set1)
 <type 'frozenset'>

~~~

#### 集合类型操作符（仅适用于可变集合）

(union) update ( |= ) 

这个更新方法从已存在的集合中添加(可能多个)成员，和 update()等价.

保留/交集更新( &= ) 

保留(或交集更新)操作保留与其他集合的共有成员，和 intersection_update()等价

差更新 ( -= ) 

对集合 s 和 t 进行差更新操作 s-=t，差更新操作会返回一个集合，该集合中的成员是集合 s 去除掉集合 t 中元素后剩余的元素。和 difference_update()等价。

对称差分更新( ^= ) 

对集合s和t进行对称差分更新操作(s^=t),对称差分更新操作会返回一个集合，该集合中的成员仅是原集合 s 或仅是另一集合 t 中的成员。和 symmetric_difference_update()等价

### 内建函数

#### 标准类型函数

##### len() 

把集合作为参数传递给内建函数 len()，返回集合的基数(或元素的个数)。

#### 集合类型工厂函数

##### set() / frozenset() 

set()和 frozenset()工厂函数分别用来生成可变和不可变的集合。如果不提供任何参数，默认会生成空集合。如果提供一个参数，则该参数必须是可迭代的，即，一个序列，或迭代器，或支持迭代的一个对象。
