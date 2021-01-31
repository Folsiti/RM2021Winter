## 1、以下类定义中哪些是类属性，哪些是实例属性？

```python
class C:
    num = 0
    def __init__(self):
        self.x = 4
        self.y = 5
        C.count = 6
```

`num = 0`是类属性

`self.x`和`self.y`是实例属性

## 2、怎么定义私有⽅法？

在类中命名时在前面加两个`_`就创建了一个私有变量/方法



## 3、尝试执行以下代码，并解释错误原因：

```python
class C:
    def myFun():
        print('Hello!')
    c = C()
    c.myFun()
```

执行代码时报错`NameError: name 'C' is not defined`，表面C未被定义

这时我发现创建c时是在`class C`里进行的，这时我把最后两行代码放到外面时，又报错`TypeError: myFun() takes 0 positional arguments but 1 was given`，我发现在`myFun()`的括号内没有`self`，因此会报错

## 4、按照以下要求定义一个游乐园门票的类，并尝试计算2个成人+1个小孩平日票价。

**要求:**

- **平日票价100元**
- **周末票价为平日的120%**
- **儿童票半价**

```python
class tickets:
    '''
    age中0表示年龄为成年；1表示未成年
    date中0表示非节假日；1表示节假日
    '''
    def set_age(self,age):
        self.age = age
    def set_date(self,date):
        self.date = date
    def money(self):
        mon = 100
        if self.age == 1:
            mon *= 0.5
        if self.date == 1:
            mon *= 1.2
        return mon
a = tickets()
a.set_age(1)
a.set_date(0)
b = tickets()
b.set_age(0)
b.set_date(0)
print(2*b.money()+a.money())
```

