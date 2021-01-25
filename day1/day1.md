### 一.思考题

#### 1.Python是怎么诞生的？Python之父是谁？

​		Python是为了继承ABC语言新的一个解释程序，其名字来源于创始人Gudio van Rossum是BBC电视剧--蒙提·派森的飞行马戏团（Monty Python’s Flying Circus）的爱好者。在ABC语言中其目标是专门为**非专业程序员**设计的，但ABC没有达到预期的结果，于是Gudio认为是**非开发**造成的，在python中避免了这一错误，并取得了很好的效果

​		Python之父也就是上一段落的Gudio van Rossum曾在Google工作为 Google 写了面向网页的代码浏览工具，后来与2019年10月31日退休，并在2020年11月13日加入微软，继续为Python社区做出贡献。

#### 2.Python和C++（或者C）的区别在哪？即为什么要学习Python，C++不香吗？

​		我认为最大的区别在于书写格式语法格式的不同，在c++中对一个变量的定义是少不了的，但在Python中，除了关键字以外的合法变量名是可以直接使用的

```C++
int a = 2;    /*c++中定义a，并对其赋值
```

```python
a = 2         #python中对a赋值/定义
```

​		在C++的代码格式中分号，各种括号是区分代码的关键，某一行缺少了分号就会报错；而在Python中，缩进是最重要的，在下面情况下，缩进可能会造成不同的结果

```python
b=0
if b == 1 :
    print("yes")
print("end")    #情况1，输出只有end
```

```python
b=0
if b == 0 :
    print("yes")
print("end")    #情况2，输出了yes和end
```

​		可见缩进在Python的重要性。

​		字符串方面，Python的功能性更好的拓展，拥有很多字符串运算符

| 操作符    | 描述                                                         |
| --------- | :----------------------------------------------------------- |
| +         | 字符串连接                                                   |
| *         | 重复输出                                                     |
| []        | 通过索引获取字符串中字符                                     |
| [ : ]     | 截取字符串中的一部分，遵循**左闭右开**原则，str[0:2] 是不包含第 3 个字符的。 |
| in/not in | 成员运算符 - 如果字符串中包含/不包含给定的字符返回 True      |
| r/R       | 原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 **r**（可以大小写）以外，与普通字符串有着几乎完全相同的语 |

​		另一方面Python的生态库与C++的不同，其最大优势就是开源，使其发展可以在千万人协作的基础上更快更好地进行优化，具有更长的生命周期和更强大的功能。

#### 3.相较于Python2，Python3做了哪些大的改进？

​		1.在py2中print是关键字，将括号里的看成一个整体；而在py3中是个函数，将结果接收字符串作为参数处理

​		2.高级的解包操作， 如 `a, b, *c= range(10)`

​		3.限定关键字参数， 参数特别多的时候指定参数以防搞混

​		4.性能优化

​		5.python3 引入了 asyncio 来进行异步IO编成

### 二.练习题

#### 1.怎样对python中的代码进行注释？

​		1.单行注释：结尾后加"#"+注释

```python
a = 3     #此处为注释
```

​		2.多行注释：开头前和结尾后一行写下"""或'''

```python
a = 2
"""
此处为注释
此处为注释
"""
a = 3
```

```python
a = 2
'''
此处为注释
此处为注释
'''
a = 3
```

#### 2.python有哪些运算符，这些运算符的优先级是怎样的？

| 运算符说明 | Python运算符            | 优先级 | 结合性 |
| ---------- | ----------------------- | ------ | ------ |
| 小括号     | ( )                     | 19     | 无     |
| 索引运算符 | x[i] 或 x[i1: i2 [:i3]] | 18     | 左     |
| 属性访问   | x.attribute             | 17     | 左     |
| 乘方       | **                      | 16     | 右     |
| 按位取反   | ~                       | 15     | 右     |
| 符号运算符 | +（正号）、-（负号）    | 14     | 右     |
| 乘除       | *、/、//、%             | 13     | 左     |
| 加减       | +、-                    | 12     | 左     |
| 位移       | >>、<<                  | 11     | 左     |
| 按位与     | &                       | 10     | 右     |
| 按位异或   | ^                       | 9      | 左     |
| 按位或     | \|                      | 8      | 左     |
| 比较运算符 | ==、!=、>、>=、<、<=    | 7      | 左     |
| is 运算符  | is、is not              | 6      | 左     |
| in 运算符  | in、not in              | 5      | 左     |
| 逻辑非     | not                     | 4      | 右     |
| 逻辑与     | and                     | 3      | 左     |
| 逻辑或     | or                      | 2      | 左     |
| 逗号运算符 | exp1, exp2              | 1      | 左     |

Ps:优先级数字越大的优先级越高

#### 3.python 中 `is`, `is not` 与 `==`, `!=` 的区别是什么？

首先`is`，`is not`比较的是两个对象的`id`值是否相等，也就是比较俩对象是否为同一个实例对象，是否指向同一个内存地址，`id(object)`函数是返回对象`object`在其生命周期内位于内存中的地址，`id`函数的参数类型是一个**对象**。因此`is`和`is not`的参数类型也是**对象**，也就是比较俩对象是否为同一个实例对象，是否指向同一个内存地址。

而`==`和`!=`比较的是两个对象的内容是否相等

```python
a = [4,5,6]
b = [4,5,6]
print(a == b)       #True
print(a is b)       #False
print(id(a))        #2375820246016
print(id(b))        #2375821562688
c = 3
d = 4
print(c == d)       #True
print(c is d)       #True
print(id(c))        #140718064346976
print(id(d))        #140718064346976
```

虽然每一次的id数值是不一样的，但可以发现`c`和`d`的id永远都是一样的，而`a`和`b`的永远不一样

#### 4.python 中包含哪些数据类型？这些数据类型之间如何转换？

**1.类型：**

​	数字类：

​			`int`整型、`long`长整型、`float`浮点数、`complex`复数

​	布尔类：

​			`bool`布尔值

​	字符串:

​			`str`类

​	列表：

​			`list`

**2.转换：**

​	1、`list`转`str`

​			假设有一个名为test_list的list，转换后的str名为test_str

​			则转换方法：

​			`est_str = "".join(test_list)`

​	2、`str`转`list`

​			假设有一个名为test_str的str，转换后的list名为test_list

​			则转换方法：

​			`test_list=list(test_str)`

​	3、对于一般的情况将 a 转成目标类型

​			如转int整型 `int(a)`其他情况类似
