# 图像的基础操作、色彩空间

1.选取区域：

​	通过ROI获得 如`something = img[0:300, 70:350]`

2.获取单色通道：

​	`b,g,r = cv.split(img)`

3.合并通道

​	`img = cv.merge((b,g,r))`

4.BGR to HSV

​	`hsv_img = cv.cvtColor(bgr_img, cv.COLOR_BGR2HSV)`

5.HSV to BGR

​	和上一个相似，`bgr_img = cv.bgrColor(bgr_img, cv.COLOR_HSV2BGR)`

## **思考题**：

### HSV和BGR三原色在图片信息存储的差别在哪？

HSV表示色调（H），饱和度（S），明度（V） 也称六角锥体模型

BGR也就是蓝绿红，

他们储存信息都是用列表储存的，差别仅在于储存的信息代表的不同

![](C:\Users\folsi\Desktop\视觉组作业\IMG\20200117163829611.jpg)

## **练习题**：

### 编写一段程序实现以下功能:

代码调用电脑摄像头，寻找视野中任意颜色（自定）并具有一定大小的物体，并用矩形框处，最后显示在图像上；

```python
import cv2 as cv
import numpy as np
cap = cv.VideoCapture(0, cv.CAP_DSHOW)

heart = np.array((
	[0, -1, 0],
	[-1, 5, -1],
	[0, -1, 0]), dtype="int")


while True:
    ret, frame = cap.read()
    hsv = cv.cvtColor(frame, cv.COLOR_BGR2HSV)
    hsv = cv.filter2D(hsv, -1, heart)
    lower = np.array([156, 43, 46])
    upper = np.array([180, 255, 255])
    mask = cv.inRange(hsv, lower, upper)
    (cnt_s, _) = cv.findContours(mask.copy(),cv.RETR_EXTERNAL,cv.CHAIN_APPROX_SIMPLE)
    if len(cnt_s) > 0:
        cnt = sorted(cnt_s, key=cv.contourArea, reverse=True)
        for i in cnt:
            if len(i) >60:
                rect = np.int32(cv.boxPoints(cv.minAreaRect(i)))
                cv.drawContours(frame, [rect], -1, (0, 0, 0), 3)
    cv.imshow('frame', frame)
    cv.imshow('mask', mask)
    if cv.waitKey(1) == ord('1'):
        break
cv.destroyAllWindows()
```

