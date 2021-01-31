## 怎么给函数编写⽂档？

方法一：

```python
def function1(inputt):
    "文档"
```

方法二：

```python
def function2(inputt):
    """
    文档
    :param name:
    :return:
    """
```

调用：

`function.__doc__`

## 怎么给函数参数和返回值注解？

函数参数注解：

​	在参数后加冒号标注类型如`(inputa:int, inputb:str)`

返回值注解：

​	在函数参数的括号后面加上箭头`->`，也就是一个减号一个大于符号在标注类型，如`def functionc(x) -> int:`

变量注解：

​	除此之外，变量也有注解，方法类似：`y : int = 3`

## 闭包中，怎么对数字、字符串、元组等不可变元素更新。

使用`nonlocal`关键字，若外界有一变量a，在闭包中使用`nonlocal a = 100`进行更新

## 分别根据每一行的首元素和尾元素大小对二维列表 a = [[6, 5], [3, 7], [2, 8]] 排序。(利用lambda表达式)

```python
a = [[6, 5], [3, 7], [2, 8]]
b = []
b.extend(a)
b.sort(key=lambda x:x[0])
print(b)
c = []
c.extend(a)
c.sort(key=lambda x:x[1])
print(c)
```



## 利用python解决汉诺塔问题？

```python
def HanNuo(n, a, b, c):
    if n == 1:
        print("将盘子",n,"从 ",a," -----> ",c)
    else:
        HanNuo(n - 1, a, c, b)
        print("将盘子",n,"从 ",a," -----> ",c)
        HanNuo(n - 1, b, a, c)
HanNuo( 64 ,'a','b','c')
```

