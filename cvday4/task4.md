### **练习题**：

 将下面纸张通过变换调节至正中央水平竖直放置，最终呈现的图片效果上要保留白纸外的区域：（源文件在img/task_image/task3_1）

![](https://github.com/GRF-Sunomikp31/Robomaster-skyteam/blob/main/2021%E5%AF%92%E5%81%87%E8%A7%86%E8%A7%89%E7%BB%84%E6%A2%AF%E9%98%9F%E5%AD%A6%E4%B9%A0%E8%AE%A1%E5%88%92/%E7%AC%AC%E4%BA%8C%E5%91%A8%20opencv%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/Img/04/task3_1.jpg)

### 步骤：

1.找到a4纸的四个点的像素坐标，这里我采用通过Photoshop来查看像素坐标的方法

![](https://github.com/Folsiti/RM2021Winter/blob/main/cvday4/img/ps2.png)

2.确定输出图像大小，我用ps查看了a4的图像像素大小

![](https://github.com/Folsiti/RM2021Winter/blob/main/cvday4/img/a4.png)

应为`2480*3508`太大了，不方便看，于是改用按原比例缩小一半为`1240*1754`

3.通过`getPerspectiveTransform`建立透视变换，并用`warpPerspective`得到图片

### 代码：

```python
import cv2 as cv
import numpy as np

img = cv.imread('C:/BG/task3_1.jpg')
rows, cols, ch = img.shape
point1 = np.array([[2096, 588], [3389, 1100], [444, 1576], [1984, 2808]], dtype="float32")
point2 = np.array([[0, 0], [1240, 0], [0, 1754], [1240, 1754]], dtype="float32")
M = cv.getPerspectiveTransform(point1, point2)
out = cv.warpPerspective(img, M, (1240, 1754))
cv.imwrite('C:/BG/put.jpg',out)
```

Ps:在读入图片时如果在路径后加上个0，也就是`imread(path,0)`图片将会变成灰度图，且shape将只有2个参数
