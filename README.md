## **Advanced Lane Finding Project**

The goals / steps of this project are the following:

- Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
- Apply a distortion correction to raw images.
- Use color transforms, gradients, etc., to create a thresholded binary image.
- Apply a perspective transform to rectify binary image ("birds-eye view").
- Detect lane pixels and fit to find the lane boundary.
- Determine the curvature of the lane and vehicle position with respect to center.
- Warp the detected lane boundaries back onto the original image.
- Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Camera Calibration

#### 1. 图像矫正

使用opencv函数获取角点并计算系数矩阵,然后调用undistort进行矫正棋盘

![角点](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E6%89%BE%E5%88%B0%E8%A7%92%E7%82%B9.png)

![矫正](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E7%9F%AB%E6%AD%A3%E4%BE%8B%E5%AD%90.png)

### Pipeline (single images)

#### 1. 测试

![测试矫正](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E6%B5%8B%E8%AF%95.png)

#### 2. 获取二值图像

使用sobel算子计算梯度并测试不同颜色通道下使用阈值的效果最重选取效果较好的几种进行组合

测试sobel与v通道阈值效果

![sobel&v](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/sobel%20%26%20v.png)

#### 3.透视变换



```python
src = np.float32([(560,464),
                  (707,464), 
                  (275,682), 
                  (1049,682)])
dst = np.float32([(450,0),
                  (830,0),
                  (450,720),
                  (830,720)])
```

This resulted in the following source and destination points:

|  Source   | Destination |
| :-------: | :---------: |
| 560, 464  |   450, 0    |
| 707, 464  |   830, 0    |
| 275, 682  |  450, 720   |
| 1049, 682 |  830, 720   |

![透视变换](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E8%A7%86%E8%A7%92%E5%8F%98%E6%8D%A2.png)

#### 4. 拟合车道线

使用直方图,在峰指附近进行滑窗选取非零值

![直方图](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E7%9B%B4%E6%96%B9%E5%9B%BE.png)

#### 5. 计算曲率半径和偏移距离

在`calc_curv_rad_and_center_dist`函数中,二次多项式拟合得到

![滑窗拟合](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E6%BB%91%E7%AA%97%E6%8B%9F%E5%90%88.png)

#### 6. 测试

绘制车道线与可行区域

![车道线](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E8%BD%A6%E9%81%93%E7%BA%BF%E7%BB%98%E5%88%B6.png)

------

### Pipeline (video)

#### 1. 视频测试

Here's a [link to my video result](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/project_video_output.mp4)
