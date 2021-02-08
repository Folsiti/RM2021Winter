### **练习题**：

 创建一个视频用来演示一幅图如何平滑的转换成另一幅图（使用函数[cv.addWeighted](https://docs.opencv.org/4.1.0/d2/de8/group__core__array.html#gafafb2513349db3bcff51f54ee5592a19)）：

### 代码：

```python
import cv2 as cv
import numpy as np

imga = cv.imread('C:\BG\Cyberpunk2077_Wallpapers_KangTao_1920x1080_ZHS.png')
imgb = cv.imread('C:\BG\Cyberpunk2077_Wallpapers_Militech_1920x1080_ZHS.png')
fourcc = cv.VideoWriter_fourcc('M', 'P', '4', 'V') #解码器
out = cv.VideoWriter('C:\BG\out.mp4', fourcc, 60, (1920, 1080), isColor=True)
alphaValue = 0.0

'''
渐变前
'''
for i in range(120):
    out.write(imgb)       #加载2秒
'''
渐变中
'''
while alphaValue <= 1.0:
    imgout = cv.addWeighted(imga, alphaValue, imgb, 1 - alphaValue, 0)
    alphaValue += 0.005
    out.write(imgout)
'''
渐变后
'''
for i in range(120):
    out.write(imga)       #加载两秒
print("Saving...")
out.release()
print("Finish")
```

### 效果：

B站链接：https://www.bilibili.com/video/BV1if4y1r7aJ/

~~（懒得加BGM了）~~

### 题外话：

之前输出的视频一直没有不能播放，搞了半天原来是解码器的问题。MP4V这个解码器同样可以输出avi格式的视频

