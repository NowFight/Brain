# Chapter 2

## 函数
Python是通过引用方式传递参数的，这意味着函数内对参数的修改会影响到原始对象。不过事实上只是可变对象会受此影响，对于不可变对象来说，其行为和传值调用一样。

## 模块
模块是一种组织形式，它将彼此有关系的Python代码组织到一个独立文件中。
模块可以包含可执行代码，函数和类或者这些的组合。当创建一个Python源文件，模块的名字就是不带后缀名的文件名。
在一个模块创建后，可以使用import语句导入模块来使用。

## 实用函数
**dir([obj])**
:   显示对象的属性，如果没有提供参数， 则显示全局变量的名字	

**help([obj])**
:   以一种整齐美观的形式 显示对象的文档字符串， 如果没有提供任何参数， 则会进入交互式帮助。

**int(obj)**
:   将一个对象转换为整数 

**len(obj)**
:   返回对象的长度

**open(fn, mode)**
:   以 mode('r' = 读， 'w'= 写)方式打开一个文件名为 fn 的文件 

**range([[start,]stop[,step])**   	
:   返回一个整数列表。起始值为 start, 结束值为 stop - 1; start 默认值为 0， step默认值为1。 

**raw_input(str)**
:   等待用户输入一个字符串， 可以提供一个可选的参数 str 用作提示信息。 

**str(obj)**
:   将一个对象转换为字符串 

**type(obj)**
:   返回对象的类型（返回值本身是一个 type 对象！） 
