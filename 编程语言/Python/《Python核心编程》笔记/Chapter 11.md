# Chapter 11 {#chapter_11}

## 函数

### 返回值与函数类型

过程是简单、特殊、没有返回值的函数，python中的过程，对应的返回对象类型是**None**。python里的函数可以返回一个值或者对象。

当没有显式地返回元素或者返回None时，python会返回一个None，如果函数返回多个对象，python把他们聚集起来并以一个元组返回。

许多静态类型的语言主张一个函数的类型就是其返回值的类型。在python中，由于python是动态地确定类型而且函数能返回不同类型的值，所以没有进行直接的类型关联。

### 调用函数

#### 参数组

Python允许通过不显式指定参数的方式调用一个函数，相应的方法是通过一个把元组（非关键字参数）或字典（关键字参数）作为参数组传递给函数。

基本上可以将所有参数放进一个元组或者字典中，仅仅用这些装有参数的容器来调用一个函数，而不必显式地将它们放在函数调用中。

~~~

func(*tuple_grp_nonkw_args, **dict_grp_kw_args)

~~~

#### 关键字参数

关键字参数的概念仅仅针对函数的调用。通过使用字典实现关键字参数，这种理念是让调用者通过函数调用中的参数名字来区分参数。这样规范允许参数缺失或者不按顺序,因为解释器能通过给出的关键字来匹配参数的值。

~~~

def function(arg1, arg2):
    print arg1 + arg2

function(arg2 = "arg1", arg2 = "arg2")

~~~

### 创建函数

#### def语句

~~~

def function_name(arguments): 
	"function_documentation_string" 
	function_body_suite 

~~~

#### 声明与定义比较

在某些编程语言里,函数声明和函数定义区分开的。一个函数声明包括提供对函数名，参数的名字（传统上还有参数的类型），但不必给出函数的任何代码，具体的代码通常属于函数定义的范畴。在声明和定义有区别的语言中，往往是因为函数的定义可能和其声明放在不同的文件中。python将这两者视为一体，函数的子句由声明的标题行以及随后的定义体组成的。

#### 前向引用

和其他高级语言类似,Python也不允许在函数未声明之前,对其进行引用或者调用。

#### 函数属性

函数属性是python一个使用了句点属性标识并拥有名字空间的领域。

~~~

function_name.attribute = value

~~~

函数属性可以在运行时刻访问它，但是不能在函数的定义中访问属性。

函数属性是在Python 2.1中添加的。

### 内部/内嵌函数

在函数体内创建另外一个函数（对象）是完全合法的。这种函数叫做内部/内嵌函数。因为python支持静态地嵌套域（在 2.1 中引入但是到 2.2 时才是标准）。

内嵌函数对于较老的python版本没有什么意义，那些版本中只支持全局和一个局部域。

一种创建内部函数的方法：

~~~

def outside():
	'out side function'
	def inside():
		'in side function'
		 ...
	...

~~~

内部函数的整个函数体都在外部函数的作用域之内。如果没有通过外部函数对其内部函数进行调用，那么除了在函数体内，任何地方都不能对其进行调用。

另外一个函数体内创建函数对象的方式是使用 **lambda** 语句。

如果内部函数的定义包含了在外部函数里定义的对象的引用（这个对象甚至可以是在外部函数之外），内部函数就被称为闭包（closure）。

### 函数（方法）修饰器

装饰器是在函数调用之上的修饰。这些修饰仅是当声明一个函数或者方法的时候，才会应用的额外调用。

装饰器的语法以 @ 开头，接着是装饰器函数的名字和可选的参数。紧跟着装饰器声明的是被修饰的函数，和装饰函数的可选参数。

~~~

@decorator(dec_opt_args) 
def func2Bdecorated(func_opt_args): 
    ...

~~~

修饰器可以如函数调用一样“堆叠“起来:

~~~

@deco2 
@deco1 
def func(arg1, arg2, ...): 
    pass 

~~~

这和创建一个组合函数是等价的:

~~~

def func(arg1, arg2, ...): pass 
func = deco2(deco1(func))

~~~

#### 有参数和无参数的修饰器

无参修饰器

~~~

@deco 
def foo():
	function body

~~~

有参修饰器

~~~

@decomaker(deco_args) 
def foo():
	function body

~~~

修饰器的目的是为了将函数作为参数传递进来，然后对这个函数进行包装，并返回一个函数对象，可以为函数的运行配置合适的运行环境，实际上修饰器就是一个函数，它可以接受函数对象，并返回一个函数对象。

#### 传递函数

函数是可以被引用的（访问或者以其他变量作为其别名），也作为参数传入函数，以及作为列表和字典等等容器对象的元素。

函数有一个独一无二的特征使它同其他对象区分开来，那就是函数是可调用的，可以通过函数操作来调用他们。函数作为一个对象，可以将函数对象传递给函数，也可以将函数对象的引用赋值给一个变量。

### 形式参数

python函数的形参集合由在调用时要传入函数的所有参数组成，这参数与函数声明中的参数列表精确的配对。这些参数包括了所有必要参数(以正确的定位顺序来传入函数的），关键字参数（以顺序或者不按顺序传入，但是带有参数列表中曾定义过的关键字），以及所有含有默认值，函数调用时不必要指定的参数。

#### 位置参数

位置参数必须以在被调用函数中定义的准确顺序来传递，没有任何默认参数的话，传入函数的参数的数目必须和声明的数字一致。

#### 默认参数

默认参数是如果在函数调用时没有为参数提供值则使用预先定义的的默认值。

python中使用默认值声明变量的语法是所有的位置参数必须出现在任何一个默认参数之前。默认参数的语法是每个默认参数都紧跟着一个用默认值：

~~~

def function(arg, arg1_name = value, arg2_name = value)

~~~

注意：参数出现的顺序必须是和上述一样的顺序。

#### 可变长度的参数


如果需要用函数处理可变数量参数的情况，这时可使用可变长度的参数列表。变长的参数在函数声明中不是显式命名的，因为参数的数目在运行时之前是未知的，甚至在运行的期间，每次函数调用的参数的数目也可能是不同的。


##### 非关键字可变长参数

当函数被调用的时候，所有的位置参数的值赋给了在函数声明中相对应的局部变量。剩下的非关键字参数按顺序插入到一个元组中便于访问。可变长的参数元组必须在位置和默认参数之后。

非关键字可变长参数的函数的语法：

~~~

def function_name(arg1, arg2, *vargs_tuple): 
	"function_documentation_string" 
	function_body_suite

~~~

星号(\*)操作符之后的形参将作为元组传递给函数,元组保存了所有传递给函数的"额外"的参数。如果没有给出额外的参数，元组为空。

##### 关键字可变长参数

如果传入的是不定数目的关键字参数，参数被放入一个字典中，字典中键为参数名，值为相应的参数值。这可以用来处理关键字参数数目没有指定的情况。

~~~

def function_name(formal_args, *vargst, **vargsd): 
	function_documentation_string function_body_suite 

~~~

这种方式的参数主要处理未指定数目的参数，在存在默认参数和位置参数的地方也可以使用关键字参数来指定参数名和参数的值，可以实现灵活的改变参数排列的位置。

关键字和非关键字可变长参数都有可能用在同一个函数中，只要关键字字典是最后一个参数并且非关键字元组先于它之前出现。 这些参数包括标准的位置参数和关键字参数，所以在python中允许的函数调用的完整语法为：

~~~

func(positional_args, keyword_args, *tuple_grp_nonkw_args, **dict_grp_kw_args) 

~~~

## 函数式编程

### 匿名函数与lambda

python允许用**lambda**关键字创造匿名函数。

匿名函数不需要以标准的方式来声明，除非赋值给一个局部变量，这样的对象不会在任何的名字空间内创建名字

~~~

lambda [arg1[, arg2, ... argN]]: expression 

 >>> f = lambda a1, a2: a1 + a2
 >>> f(1, 2)
 3

~~~

参数是可选的，如果使用的参数话，参数通常也是表达式的一部分。

### lambda 表达式返回可调用的函数对象。 

可以像其他函数一样使用的函数对象。它们可被传入给其他函数，用额外的引用别名化，作为容器对象以及作为可调用的对象被调用（如果需要的话，可以带参数）。当被调用的时候，如果给定相同的参数的话，这些对象会生成一个和相同表达式计算结果等价的结果。它们和那些返回等价表达式计算值相同的函数是不能区分的。

这种语句的目的是由于性能的原因，在调用时绕过函数的栈分配。lambda表达式运作起来就像一个函数，当被调用时，创建一个框架对象。


#### 内建函数 apply()、filter()、map()、reduce()

apply(func[, nkw][, kw])
:   用可选的参数来调用func，nkw为非关键字参数，kw关键字参数；返回值是函数调用的返回值。[a]，在Python 3中被支持

filter(func, seq)
:   调用一个布尔函数func来迭代遍历每个seq中的元素；返回一个使func返回值为Ture的元素的序列。[b]
    在Python 2里，filter()方法返回一个列表，这个列表是通过一个返回值为True的函数来检测序列里的每一项得到的。在Python 3里，filter()函数返回一个迭代器，不再是列表。

map(func, seq1[,seq2...])
:   将函数func作用于给定序列（s)的每个元素，并用一个列表来提供返回值；如果func为None，func表现为一个身份函数，返回一个含有每个序列中元素集合的n个元组的列表。[b]
    在Python 3中map()函数现在返回一个迭代器。

reduce(func, seq[, init]) 
:   将二元函数作用于seq序列的元素，每次携带一对（先前的结果以及下一个序列元素），连续的将现有的结果和下一个值进行func处理，
    最后减少我们的序列为一个单一的返回值；如果初始值init给定，第一个比较会是init和第一个序列元素而不是序列的头两个元素。
    在Python 3里，reduce()函数已经被从全局名字空间里移除了，它现在被放置在fucntools模块里。

a.可以有效的取代1.6，在其后的python版本中逐渐淘汰。	    
b.由于在python2.0中，列表的综合使用的引入，部分被摈弃。	    

~~~

 >>> filter(lambda arg : arg > 10, [1, 2, 20, 30])
 [20, 30]

 >>> def func(a):
	return a ** 2

 >>> map(func, [1, 2, 3, 4])
 [1, 4, 9, 16]

~~~

## 变量作用域

### globa 语句

如果将全局变量的名字声明在一个函数体内的时候，全局变量的名字能被局部变量给覆盖掉。为了明确地引用一个已命名的全局变量，必须使用global语句。global的语法如下:

~~~

global var1[, var2[, ... varN]]]

~~~

### 闭包

如果在一个内部函数里，对在外围函数作用域的变量进行引用，那么内部函数就被认为是 closure。定义在外部函数内的但由内部函数引用或者使用的变量被称为自由变量。

闭包将内部函数自己的代码和作用域以及外部函数的作用结合起来。闭包的词法变量不属于全局名字空间域或者局部，而是属于其他的名字空间

~~~

 >>> def counter(start_at=0): 
 	count = [start_at] 
 	def incr(): 
 		count[0] += 1 
 		return count[0] 
 	return incr
 
 >>> c = counter()	#返回一个函数对象

~~~

内部函数中使用了自由变量count，则通过c=counter()返回一个函数对象的时候，其c引用的函数对象在counter()中被定义了，当对c绑定的函数对象进行函数执行函数操作的时候，其将会从静态嵌套域中获取自由变量的值，而每次执行c()的时候，c引用的函数对象所关联的静态嵌套域中的count[0]都会加1，实现了计数功能。静态嵌套域没有随着counter()运行结束而销毁，而是和返回的函数对象相关联的。
 
### 作用域和lambda

python的lambda匿名函数遵循和标准函数一样的作用域规则。一个lambda表达式定义了新的作用域，就像函数定义，所以这个作用域只能被lambda函数自己访问的。

### 生成器

挂起返回出中间值并多次继续的协同程序被称为**生成器**。从句法上讲，生成器是一个带**yield**语句的函数。一个函数或者子程序只返回一次，但一个生成器能暂停执行并返回一个中间的结果。

与迭代器相似，生成器以另外的方式来运作：当到达一个真正的返回或者函数结束没有更多的值返回（当调用next())，一个StopIteration异常就会抛出。

~~~

 >>> def generator(end = 100):
	while end > 0:
		yield end
		end = end - 1
	return

 >>> for i in generator(10):
    print i,
 10 9 8 7 6 5 4 3 2 1

~~~
