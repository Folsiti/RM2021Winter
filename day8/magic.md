## 1、上面提到了许多魔法方法，如__new__,__init__, __str__,__rstr__,__getitem__,__setitem__等等，请总结它们各自的使用方法。

1.`new`是创建对象时会执行的方法，当你继承一些不可变的 class 时（比如`int, str, tuple`）， 提供给你一个自定义这些类的实例化过程的途径

2.`init`为构造函数，当一个实例被创建的时候调用的初始化方法

3.`del`为析构函数，对象在被回收时会被调用（程序结束时，系统进行回收也会运行）

4.`call`为调用函数，可以像调用函数一样调用类

```python
class Student:
    def __init__(self,name):
        self.name = name
    def __call__(self, *args, **kwargs):
        print(sum(args))
a = Student(2)
print()
a(1,2)
```

5.`str`返回一个字符串，方便`print()`函数查看对象。**补充**：创建类时，系统有一个默认的`str`方法，自己写时会被覆盖

6.`len`设置计量对象长度的方法，方便`len()`

7.`iter`改写迭代器，用于`for`语句中`i in xxx`的迭代：

```python
class Student:
    cn = 0
    en = 0
    cpp = 0
    def __init__(self,name:str):
        self.name = name
    def __iter__(self):
        return([self.cn, self.en,self.cpp])
a = Student("Xiao Ming")
for i in a.__iter__():
    print(i)
```

8.`getitem`用于设置返回值，如：

```python
class Student:
    def __init__(self,name:str):
        self.name = name
    def __getitem__(self, item):
        if item == 'name':
            return self.name
        else:
            return None
a = Student("Xiao Ming")
print(a['name'])
```

9.`setitem`与`getitem`相似，用于改变对象属性（赋值）

10.`delitem__(self, key)`定义删除容器中指定元素的行为，相当于`del self[key]`

## 2、利用python做一个简单的定时器类

要求:

定制一个计时器的类。
start和stop方法代表启动计时和停止计时。
假设计时器对象t1，print(t1)和直接调用t1均显示结果。
当计时器未启动或已经停止计时时，调用stop方法会给予温馨的提示。
两个计时器对象可以进行相加：t1+t2。
只能使用提供的有限资源完成。

```python
import time
class timer():
    def __init__(self):
        self.text =str()
        self.lasted = []
        self.begin = 0
        self.end = 0
    def start(self):
        self.begin = time.localtime()
    def stop(self):
        self.end = time.localtime()
        self.out()
    def __add__(self, other):
        return str(int(self.text)+int(other.text))
    def out(self):
        self.oout = []
        for i in range(max(len(self.end),len(self.begin))):
            self.oout.append(self.end[i] - self.begin[i])
            self.text += str(self.oout[i])
    def __str__(self):
        return str(int(self.text))
```



## 3.补充：特殊成员

`doc`类文档，无需def，在类内用三引号写文档，调用时即可看到

`dict`用于展示成员属性，包括私有属性

