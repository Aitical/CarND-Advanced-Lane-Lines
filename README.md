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

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

use `findChessboardCorners` to get corner points

use  `cornerSubPix` to identify

use `drawChessboardCorners`  to visualize

![角点](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E6%89%BE%E5%88%B0%E8%A7%92%E7%82%B9.png)

![矫正](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E7%9F%AB%E6%AD%A3%E4%BE%8B%E5%AD%90.png)

### Pipeline (single images)

#### 1.Provide an example of a distortion-corrected image.

use the matrix chreated before and `cv2.undistort` to test on another image

![测试矫正](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E6%B5%8B%E8%AF%95.png)

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result.

try to test  Sobel and some different color channels 

![sobel&v](https://github.com/Aitical/CarND-Advanced-Lane-Lines/blob/master/pic/sobelandhsv-v.png?raw=true)

different color channels

![different channels](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/channels.png)

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

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

![透视变换](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/warp.png)

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

using the histogram of the half bottom image 

![直方图](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E7%9B%B4%E6%96%B9%E5%9B%BE.png)

in `sliding_window_polyfit` function to get pixels index

![滑窗拟合](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/%E6%BB%91%E7%AA%97%E6%8B%9F%E5%90%88.png)

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

in `calc_curv_rad_and_center_dist` function

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

![车道线](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/pic/pipeline.png)

------

### Pipeline (video)

#### 1. 视频测试

Here's a [link to my video result](https://raw.githubusercontent.com/Aitical/CarND-Advanced-Lane-Lines/master/project_video_output.mp4)
