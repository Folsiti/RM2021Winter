## 1、假设你获取了用户输入的日期和时间如`2020-1-21 9:01:30`，以及一个时区信息如`UTC+5:00`，均是`str`，请编写一个函数将其转换为timestamp：

### 题目说明:

```python
"""
   
Input file
example1: dt_str='2020-6-1 08:10:30', tz_str='UTC+7:00'
example2: dt_str='2020-5-31 16:10:30', tz_str='UTC-09:00'
   
Output file
result1: 1590973830.0
result2: 1590973830.0
"""
   
   
def to_timestamp(dt_str, tz_str):
    # your code here
        pass
```

### 代码：

```python
import re
from datetime import *

def to_timestamp(dd, ssq):
    d = datetime.strptime(dd,'%Y-%m-%d %H:%M:%S')
    sq = re.match(r'([UTC]+)([+-])(\d+):(\d)',ssq)
    i = int(sq.group(3))
    if sq.group(2) == '+':
        tz_utc = timezone(timedelta(hours=i))
    elif sq.group(2) == '-':
        tz_utc = timezone(timedelta(hours=-i))
    dt = d.replace(tzinfo=tz_utc)
    return dt.timestamp()
```



## 2、编写Python程序以选择指定年份的所有星期日。

### 题目说明:

```
"""
   
Input file
   2020
   
Output file
   2020-01-05                         
   2020-01-12              
   2020-01-19                
   2020-01-26               
   2020-02-02     
   -----
   2020-12-06               
   2020-12-13                
   2020-12-20                
   2020-12-27 
"""
   
def all_sundays(year):
    # your code here
    
```

### 代码：

```python
import datetime

def tomorrow(today):
    return today + datetime.timedelta(days=1)

def pd(today):
    if today.weekday() == 6:
        return True
    else:
        return False

dt = datetime.date(year=2020, month=1 , day= 1)
while dt.year == 2020:
    if pd(dt):
        print(dt)
    dt = tomorrow(dt)
```

