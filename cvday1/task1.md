# OpenCV T1

## 思考题：

### Opencv库与Matlab、halcon的区别？

​		Matlab建模方便，上手快，Opencv速度更快，

​		halcon是做机器视觉的，opencv是计算机视觉

### 为什么是import **cv2**？

​		在opencv的build/include文件夹中的只有opencv2，cv2”表示使用的是C++API

### 在显示完之后，用不用cv.destroyWindow()有什么区别？

​		如果停止窗口就意味着程序运行完，那么不加是可以的。如果程序没有运行完，没加的话窗口就会一直存在，知道程序结束

### png图片格式和jpg图片格式有什么区别？

​		压缩方式不同，jpg是jpeg的缩写，可以在不损失大部分画面的基础上压缩图片，使之达到最小格式；而png是无损的压缩形式，所以png的大小普遍比jpg的要大

## **练习题**：

### 同时显示两张不同分辨率的图片，对比他们的大小；

```python
import numpy as np
import cv2 as cv


framea = cv.imread('C:\BG\Cyberpunk2077_Wallpapers_KangTao_1600x900_ZHS.png')
frameb = cv.imread('C:\BG\Cyberpunk2077_Wallpapers_KangTao_1080x1920_ZHS.png')
cv.imshow("A",framea)
cv.imshow("B",frameb)
print(framea.shape)
print(frameb.shape)

while True:
    if cv.waitKey() == ord("q"):
        break
cv.destroyAllWindows()
```

![Image](https://github.com/Folsiti/RM2021Winter/blob/main/cvday1/imgs/Kangtao.png)

### 使用Opencv，测试一下你电脑摄像头的分辨率和帧率是多少；

```python
import numpy as np
import cv2 as cv

cap = cv.VideoCapture(0,cv.CAP_DSHOW)
ret, frame = cap.read()
print(frame.shape)
```

输出结果：`(480, 640, 3)`

则分辨率为480*640

### 利用电脑摄像头从外界拍摄一幅自己的图像，添加圆（或其他图形）给自己打码，图片右下角添加自己的网名和时间。

```python
import numpy as np
import cv2 as cv
import time

time_start = time.time()
fps_time = time.time()
centerx = 50.0
centery = 50.0
sta = (15, 15)
end = (85, 85)
b = False
fps = 0
cap = cv.VideoCapture(0,cv.CAP_DSHOW)
if not cap.isOpened():
    print("Cannot open camera")
    exit()
while True:
    ret, frame = cap.read()
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    font = cv.FONT_HERSHEY_SIMPLEX
    if time.time() - time_start >= 0.02:
        if centery <= 50 and centerx < 590:
            centerx += 13.5
            time_start = time.time()
            b = True
        elif centerx >= 590 and centery < 430:
            centery += 9.5
            time_start = time.time()
            b = True
        elif centery >= 430 and centerx > 50:
            centerx -= 13.5
            time_start = time.time()
            b = True
        elif centerx <= 50 and centery > 50:
            centery -= 9.5
            time_start = time.time()
            b = True
    if b:
        sta = (int(centerx - 35), int(centery - 35))
        end = (int(centerx + 35), int(centery + 35))
        b = False
    if (time.time() - fps_time) != 0:
        fps = int(1 / (time.time() - fps_time))
        fps_time = time.time()
    cv.putText(frame, str(fps)+"FPS", (10, 50), font, 2, (255, 255, 255), 2)
    cv.putText(frame,"Folsiti",(460,430),font,2,(255,255,0),2)
    localtime = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
    cv.putText(frame, str(localtime), (425, 465), font, 1, (255, 255, 0), 2)
    cv.rectangle(frame, sta, end, (128,128,0), 3)
    cv.imshow('frame',frame)
    if cv.waitKey(1) == ord('1'):
        break
cap.release()
cv.destroyAllWindows()
```

![Image](https://github.com/Folsiti/RM2021Winter/blob/main/cvday1/imgs/folsiti.png)
