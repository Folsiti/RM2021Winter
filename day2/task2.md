v1,v2,t,s,l = input().split() 
v1=int(v1)
v2=int(v2)
t=int(t)
s=int(s)
l=int(l)
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
