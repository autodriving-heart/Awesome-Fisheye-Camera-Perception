## Awesome-Fisheye-Camera-Perception



自动驾驶应用中，AVP(自主代客泊车）成为各大主机厂和方案供应商落地的主要发力点，其中近域的4个鱼眼相机发挥了重要作用，其和普通的2D目标检测也有一些区别和联系，这里单独重点介绍。



本仓库由[公众号【自动驾驶之心】](https://mp.weixin.qq.com/s?__biz=Mzg2NzUxNTU1OA==&mid=2247542481&idx=1&sn=c6d8609491a128233c3c3b91d68d22a6&chksm=ceb80b18f9cf820e789efd75947633aec9d2f1e8b58c29e5051c05a64b21ae63c244d54886a1&token=11182364&lang=zh_CN#rd) 团队整理，欢迎关注，一览最前沿的技术分享！

自动驾驶之心是国内首个自动驾驶开发者社区！这里有最全面有效的自动驾驶与AI学习路线（感知/定位/融合）和自动驾驶与AI公司内推机会！



### 一、Survey

Near-field Perception for Low-Speed Vehicle Automation using Surround-view Fisheye Cameras

[[Code]](https://youtu.be/ae8bCOF77uY)

Surround-View Vision-based 3D Detection for Autonomous Driving: A Survey

[[Code]](https://github.com/ApoorvRoboticist/VisionBEVDetectionSurvey)

Surround-View Cameras based Holistic Visual Perception for Automated Driving

Surround-view Fisheye Camera Perception for Automated Driving: Overview, Survey & Challenges

### 二、Dataset

KITTI-360: A Novel Dataset and Benchmarks for Urban Scene Understanding in 2D and 3D

[[Link]](https://www.cvlibs.net/datasets/kitti-360)

Learning from THEODORE:A Synthetic Omnidirectional Top-View Indoor Dataset for Deep Transfer Learning

[[Link]](https://www.tu-chemnitz.de/etit/dst/forschung/comp_vision/datasets/theodore/)

Universal Semantic Segmentation for Fisheye Urban Driving Images

[[Link]](https://github.com/Yaozhuwa/FisheyeSeg)

WoodScape: A multi-task, multi-camera fisheye dataset for autonomous driving

[[Link]](https://github.com/valeoai/WoodScape)

SynWoodScape: Synthetic Surround-view Fisheye Camera Dataset for Autonomous Driving

[[Link]](https://woodscape.valeo.com/)

### 三、Fisheye Object Detection

Woodscape Fisheye Object Detection for Autonomous Driving --CVPR 2022 0mniCV Workshop Challenge

OmniDet Surround View Cameras based Multi-task Visual Perception Network for Autonomous Driving (ICRA2021)

FisheyeDet A Self-study and Contour-based Object Detector in Fisheye Images (IEEE Access 2020)

DeepSphere Efficient spherical Convolutional Neural Network with HEALPix sampling for cosmological applications (Astronomy and Computing 2019)

Kernel Transformer Networks for Compact Spherical Convolution (CVPR 2019)5.Object Detection in Equirectangular Panorama (ICPR 2018)

Spherenet Learning spherical representations for detection and classification in omnidirectional images(ECCV2018)

Spherical CNNs on unstructured grids (ICLR 2019)

WoodScape A multi-task, multi-camera fisheye dataset for autonomous driving (ICCV 2019)

Surround-view Fisheye BEV-Perception for Valet Parking: Dataset, Baseline and Distortion-insensitive Multi-task Framework

### 四、Fisheye Semantic Segmentation

Semantic Segmentation of Panoramic Images Using a Synthetic Dataset (SPIE 2019)

Restricted Deformable Convolution based Road Scene Semantic Segmentation Using Surround View

Real-Time Semantic Segmentation for Fisheye Urban Driving Images Based on ERFNet (Sensors 2019)

CNN based Semantic Segmentation for Urban Traffic Scenes using fisheye camera (IV 2017)

Deep semantic segmentation for automated driving Taxonomy, roadmap and challenges ( ITSC 2017)

## 五、Fisheye Motion Semantic Segmentation

暂无

### 六、Fisheye Depth Estimation

FisheyeDistanceNet: Self-Supervised Scale-Aware Distance Estimation using Monocular Fisheye Camera forAutonomous Driving

FisheyeDistill: Self-Supervised Monocular Depth Estimation with Ordinal Distillation for Fisheye Cameras

Monocular Fisheye Camera Depth Estimation Using Sparse LiDAR Supervision

SVDistNet: Self-Supervised Near-Field Distance Estimation on Surround View Fisheye Cameras

SynDistNet: Self-Supervised Monocular Fisheye Camera Distance Estimation Synergized with Semantic Segmentation for Autonomous Driving

BiFuse-Monocular 360。Depth Estimation via Bi-Projection Fusion(CVPR 2020)

Geometric structure based and regularized depth estimation from 360 indoor imagery (CVPR 2020)

### 七、Fisheye SLAM

Direct visual odometry for a fisheye-stereo camera (IROS 2017)

FisheyeSuperPoint: Keypoint Detection and Description Network for Fisheye Images (VISAPP 2022)

Large-Scale Direct SLAM for Omnidirectional Cameras (IROS 2015)

OmniDet: Surround View Cameras based Multi-task Visual Perception Network for Autonomous Driving (IRAL2021)

Real-Time Dense Mapping for Self-driving Vehicles using Fisheye Cameras (ICRA 2019)

### 八、Code

#### 1. Fisheye Image Correction

[HLearning/fisheye: fisheye image calibration (github.com)](https://github.com/HLearning/fisheye)

一、常见的鱼眼矫正算法

(1）棋盘格矫正法
利用棋盘格进行标定，然后计算鱼眼镜头的畸变系数以及内参,opencv中自带有fisheye模块，可以直接根据棋盘格标定结果，采用cv2.fisheye.calibrate计算畸变系数以及内参，然后使用cv2.fisheye.initUndistortRectifyMap函数计算映射矩阵，最后根据映射矩阵，使用cv2.remap进行矫正。

(2）经纬度矫正法
经纬度矫正法，可以把鱼眼图想象成半个地球，然后将地球展开成地图，经纬度矫正法主要是利用几何原理，对图像进行展开矫正，基于经纬度矫正法进行改进的矫正的算法也很多，下面主要介绍的是双径度矫正法，具体的原理参考论文《基于双经度模型的鱼眼图像畸变矫正方法》。

二、代码复现
根据作者的论文，采用python对论文进行复现（建议结果论文查看代码)，发现效果不错，不过耗时非常严重，采用最近邻插值方式，每张图耗时大概在6s左右，采用双线性插值，耗时在34s左右。
参考代码:02.double_longitude/main.py

代码优化
因为代码中进行插值涉及到了两层循环，而且每层循环，计算量都非常大，因此想到了几点优化方案.采用矩阵运算代替循环
将python代码更改为c多线程
采用gpu加速(pycuda)
想到的几种加速方案，在尝试了第一种结果方案时候，发现最近邻插值运行速度从6s降到了0.3s，果断放弃了尝试其他方案的想法，大神们也可以尝试一下其他方案。
参考代码:02.double_longitude/main_vector.py

插值方式
理论上双线性插值的结果应该优于最近邻插值，不过双线性插值方式计算量大，非常耗时，而且两种不同的插值方式，结果差异肉眼几乎无法区分，在代码改成矩阵计算后，双线性插值方式代码实现起来繁琐，所以采用了最近邻插值。



