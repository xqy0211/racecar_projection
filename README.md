# racecar_projection
本功能包为ROS下的功能包，主要节点为image_compensation和image_projection，通过名为extrinsic_camera_calibration.launch的launch文件启动节点
## 实现功能
主要用于单目车道线检测中的图像处理部分，将摄像头获取的ROS图像信息转化为opencv可用的图像信息后即可开始图像处理部分，大体包括图像的透视变换和图像增强两部分。
<br>透视变换通过cv2.getPerspectiveTransform(pts_src, pts_dst)算出投影矩阵和投影变换后的图像。
<br>图像增强部分先通过cv2.cvtColor(cv_image_compensated, cv2.COLOR_BGR2GRAY)函数将图像转化为灰度图像，之后通过cv2.calcHist([gray], [0], None, [hist_size], [0, hist_size])函数求得灰度直方图,发布/camera/image_projected_compensated，用于进行下一步的车道检测。
<br>车道检测由另一个功能报racecar_detect实现
## 参数
subscribe:  摄像头获取的ROS图像/zed/rgb/image_rect_color<br>
publish:  透视变换及图像增强后的图像/camera/image_projected_compensated
## 具体说明
透视变换是为了获得车道的鸟瞰图，方便提取车道线。<br>
效果如下：
