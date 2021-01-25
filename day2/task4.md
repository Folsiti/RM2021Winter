## 1、编写一个Python程序来查找那些既可以被7整除又可以被5整除的数字，介于1500和2700之间。

### 方案一（非最优）

#### 分析：

​		遍历1500和2700逐个分析是否能被7和5整除，由于5比7小，可以整除5的比可以整除7的多，为了减少计算量，先看是否能被7整除，再看是否能被5整除。

#### 代码：

```python
for i in range(1500,2701):
    if i%7 == 0:
        if i%5 == 0:
            print(i)
```

### 方案二

#### 分析：

​		在方案一的基础上，遍历还是花费了一些时间，由于5和7的最大公倍数为35，我们可以在通过遍历的方式找到第一个既可以被7整除又可以被5整除的数字之后循环相加35，最终超过2700时停止。

#### 代码：

```python
i = 0     #初始值，放报错
for i in range(1500,2701):
    if i%7 == 0:
        if i%5 == 0:
            print(i)
            break
while (i <= 2700):
    i+=35
    print(i)
```

## 2、龟兔赛跑游戏

### 题目描述：

​		话说这个世界上有各种各样的兔子和乌龟，但是研究发现，所有的兔子和乌龟都有一个共同的特点——喜欢赛跑。于是世界上各个角落都不断在发生着乌龟和兔子的比赛，小华对此很感兴趣，于是决定研究不同兔 子和乌龟的赛跑。他发现，兔子虽然跑比乌龟快，但它们有众所周知的毛病——骄傲且懒惰，于是在与乌龟的比赛中，一旦任一秒结束后兔子发现自己领先t米或以 上，它们就会停下来休息s秒。对于不同的兔子，t，s的数值是不同的，但是所有的乌龟却是一致——它们不到终点决不停止。

然而有些比赛相当漫长，全程观看会耗费大量时间，而小华发现只要在每场比赛开始后记录下兔子和乌龟的数据——兔子的速度v1（表示每秒兔子能跑v1 米），乌龟的速度v2，以及兔子对应的t，s值，以及赛道的长度l——就能预测出比赛的结果。但是小华很懒，不想通过手工计算推测出比赛的结果，于是他找 到了你——清华大学计算机系的高才生——请求帮助，请你写一个程序，对于输入的一场比赛的数据v1，v2，t，s，l，预测该场比赛的结果。

输入:

输入只有一行，包含用空格隔开的五个正整数v1，v2，t，s，l，其中(v1,v2< =100;t< =300;s< =10;l< =10000且为v1,v2的公倍数)

输出:

输出包含两行，第一行输出比赛结果——一个大写字母“T”或“R”或“D”，分别表示乌龟获胜，兔子获胜，或者两者同时到达终点。

第二行输出一个正整数，表示获胜者（或者双方同时）到达终点所耗费的时间（秒数）。

样例输入：

10 5 5 2 20

样例输出

D 4

### 分析：

​		在未到达终点前的位移比较好计算，重点分析兔子的规律即可。随后的判断也比较简单，检测两者的位移即可

### 代码：

```python
v1=int(input()) #rabbit speed
v2=int(input()) #turtle speed
t=int(input()) #the distance of rabbit and turtle when rabbit will sleep
s=int(input()) #rabit sleep time
l=int(input()) #total length
x1=x2=0 #x1:rabbit distance,x2:turtle distance
time=0
k=s
b=1
while x1 < l and x2 < l:
    if b == 1 and x1 - x2 <t:
        x1 += v1
    elif k != 0 :
        k -= 1
        b = 0
    else :
        if x1 - x2 < t:
            x1 += v1
            b = 1
            k = s
        elif k != 0:
            k = s - 1
            b = 0
    x2 += v2
    time += 1
z1 = x1 >= l
z2 = x2 >= l
if z1 and not z2 :
    print(time, " R")
elif z2 and not z1 :
    print(time, " T")
else:
    print(time, " D")

```

### 拓展：

增大难度，将l改为非v1,v2公倍数，增大判断谁先到终点的难度

### 分析：

如果l非v1,v2的公倍数，那么假设龟兔在最后一个整数秒不停止赛跑（即当两者中至少有一个超越终点时，坚持跑完这一秒），结果可能出现8种情况，情况数量多不适合简单if和else判断。若只有一者超过终点，可使用上面的简单判断。若两者都超过终点，我采用迂回的算法思路，当判断出最后一个整数秒出现时，返回到上一秒的状态，计算两者谁先到达终点。

### 代码：

```python
v1=int(input()) #rabbit speed
v2=int(input()) #turtle speed
t=int(input()) #the distance of rabbit and turtle when rabbit will sleep
s=int(input()) #rabit sleep time
l=int(input()) #total length
x1=x2=0 #x1:rabbit distance,x2:turtle distance
time=0
k=s
b=1
while x1 < l and x2 < l:
    if b == 1 and x1 - x2 <t:
        x1 += v1
    elif k != 0 :
        k -= 1
        b = 0
    else :
        if x1 - x2 < t:
            x1 += v1
            b = 1
            k = s
        elif k != 0:
            k = s - 1
            b = 0
    x2 += v2
    time += 1
z1 = x1 >= l
z2 = x2 >= l
if z1 and not z2 :
    print(float(time) - 1 + float((l - (x1 - v1)) / v1), " R")
elif z2 and not z1 :
    print(float(time) - 1 + float((l - (x2 - v2)) / v2), " T")
elif x1 == x2 == l :
    print(time," D")
else:
    m1 = float((l - (x1 - v1)) / v1)
    m2 = float((l - (x2 - v2)) / v2)
    if m1 < m2:
        print(float(time) - 1 + m1, " R")
    elif m2 < m1:
        print(float(time) - 1 + m2, " T")
    else:
        print(float(time) - 1 + m1, " D")
```

