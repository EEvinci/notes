# mmrotate调研

## MMrotate是什么？

​	在真实场景中，我们见到的图像不都是方方正正的，比如扫描的图书和遥感图像，需要检测的目标通常是**有一定旋转角度的**。这时候就需要用到**旋转目标检测**方法，对目标进行精确的定位，方便后面的识别、分析等高级任务。

​	所谓**旋转目标检测**（Rotated Object Detection），又称为有向目标检测（Oriented Object Detection），试图在检测出目标位置的同时得到目标的方向信息。

​	它通过**重新定义目标表示形式**，以及**增加回归自由度数量**的操作，实现旋转矩形、四边形甚至**任意形状的目标检测**。旋转目标检测在人脸识别、场景文字、**遥感影像**、自动驾驶、**医学图像**、机器人抓取等领域都有广泛应用。

​	遗憾的是，**现有的开源旋转目标检测代码库，往往支持的方法较少，角度定义法各不相同，并且不同代码库所依赖的关键算子、深度学习算法框架不一致。**这给代码复现、借鉴、公平对比都带来了很大的困难。

​	为了解决这些问题，**OpenMMLab 正式开源了 MMRotate！**这是一个专注于**旋转目标检测的工具箱**，它提供了高效、强大的基准模型！

## MMrotate的三大特点

MMrotate是**首个统一的旋转目标检测工具箱**

- 为当下流行的基于深度学习的**旋转目标检测算法**提供了**统一的训练、推理、评估的算法框架**
- **简洁的用户接口**与**高效、强大的基准模型**，部分实现精度超出官方版本
- 延续了 OpenMMLab 系列的**模块化风格**，继承了**高度灵活 config 功能**

## MMrotate支持的模型

目前支持的15种旋转目标检测算法如下：

-  [Rotated RetinaNet-OBB/HBB](https://github.com/open-mmlab/mmrotate/blob/main/configs/rotated_retinanet/README.md) (ICCV'2017)
-  [Rotated FasterRCNN-OBB](https://github.com/open-mmlab/mmrotate/blob/main/configs/rotated_faster_rcnn/README.md) (TPAMI'2017)
-  [Rotated RepPoints-OBB](https://github.com/open-mmlab/mmrotate/blob/main/configs/rotated_reppoints/README.md) (ICCV'2019)
-  [Rotated FCOS](https://github.com/open-mmlab/mmrotate/blob/main/configs/rotated_fcos/README.md) (ICCV'2019)
-  [RoI Transformer](https://github.com/open-mmlab/mmrotate/blob/main/configs/roi_trans/README.md) (CVPR'2019)
-  [Gliding Vertex](https://github.com/open-mmlab/mmrotate/blob/main/configs/gliding_vertex/README.md) (TPAMI'2020)
-  [Rotated ATSS-OBB](https://github.com/open-mmlab/mmrotate/blob/main/configs/rotated_atss/README.md) (CVPR'2020)
-  [CSL](https://github.com/open-mmlab/mmrotate/blob/main/configs/csl/README.md) (ECCV'2020)
-  [R3Det](https://github.com/open-mmlab/mmrotate/blob/main/configs/r3det/README.md) (AAAI'2021)
-  [S2A-Net](https://github.com/open-mmlab/mmrotate/blob/main/configs/s2anet/README.md) (TGRS'2021)
-  **[ReDet](https://github.com/open-mmlab/mmrotate/blob/main/configs/redet/README.md) (CVPR'2021)**
-  [Beyond Bounding-Box](https://github.com/open-mmlab/mmrotate/blob/main/configs/cfa/README.md) (CVPR'2021)
-  **[Oriented R-CNN](https://github.com/open-mmlab/mmrotate/blob/main/configs/oriented_rcnn/README.md) (ICCV'2021)**
-  [GWD](https://github.com/open-mmlab/mmrotate/blob/main/configs/gwd/README.md) (ICML'2021)
-  [KLD](https://github.com/open-mmlab/mmrotate/blob/main/configs/kld/README.md) (NeurIPS'2021)
-  **[SASM](https://github.com/open-mmlab/mmrotate/blob/main/configs/sasm_reppoints/README.md) (AAAI'2022)**
-  **[Oriented RepPoints](https://github.com/open-mmlab/mmrotate/blob/main/configs/oriented_reppoints/README.md) (CVPR'2022)**
-  [KFIoU](https://github.com/open-mmlab/mmrotate/blob/main/configs/kfiou/README.md) (arXiv)
-  [G-Rep](https://github.com/open-mmlab/mmrotate/blob/main/configs/g_reppoints/README.md) (stay tuned)

在 MMRotate 复现的大量旋转目标检测算法中，部分模型在 DOTA v1.0 数据集上甚至**超越了官方公布的精度**。

![img](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/ab0c20449ace9efe03ae398a32c5931a.png)

## MMrotate支持的角度定义法

- OpenCV
- 长边135°
- 长边90°

## 支持的遥感数据集

### DOTA

DOTA是用于航空图像中目标检测的大规模数据集。它可以用于开发和评估航空影像中的物体检测。对于DOTA数据集，它包含来自不同传感器和平台的2806个航拍图像。每个图像的大小在大约800×800到4000×4000像素的范围内，并且包含各种比例，方向和形状的对象。这些DOTA图像由航空影像解释专家分类为15个常见对象类别。完全注释的DOTA图像包含188、282个实例，每个实例都由任意（8自由度）四边形标记。
![在这里插入图片描述](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/20200504081118450.png)

[**DOTA**](https://captain-whu.github.io/DOTA/index.html)
[DOTA: A Large-scale Dataset for Object Detection in Aerial Images](https://arxiv.org/abs/1711.10398)

### SSDD

![在这里插入图片描述](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/20200504100937369.png)

在数据集SSDD中，一共有1160个图像和2456个舰船，平均每个图像有2.12个舰船，数据集后续会继续扩充。相比于具有20类目标的PASCAL VOC数据集，SSDD虽然图片少，但是类别只有舰船这一种，因此它足以训练检测模型。
下载链接：https://pan.baidu.com/s/1sVs63jB_aM-RbcHEaWQgTg

### HRSID

![在这里插入图片描述](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/20200506074916250.png)

该数据集是电子科技大学的苏浩在2020年1月发布数据集，HRSID是高分辨率sar图像中用于船舶检测、语义分割和实例分割任务的数据集。该数据集共包含5604张高分辨率SAR图像和16951个ship实例。ISSID数据集借鉴了Microsoft Common Objects in Context (COCO)数据集的构建过程，包括不同分辨率的SAR图像、极化、海况、海域和沿海港口。该数据集是研究人员评估其方法的基准。对于HRSID, SAR图像的分辨率分别为:0.5m, 1 m, 3 m。
下载链接：

[HRSID](https://github.com/chaozhong2010/HRSID)

### 参考文档

[遥感目标检测数据集汇总](https://blog.csdn.net/qq_35451572/article/details/105912382)

## MMrotate运行框架

同 OpenMMLab 其他算法库一样，使用**统一框架和模块化设计**实现了各个算法。一方面可以**尽量实现代码复用**，另一方面，**方便基于此框架实现新的算法**。

以下是 MMRotate 的大致框架：

![img](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/2d7168792a9441f45fe600a624ba9fe1.png)

MMRotate 主要由 4 个部分组成，**datasets、models、core 和 apis 。**

- datasets 用于数据集加载和预处理，其中包含**训练所需的数据集**，旋转框数据增广的 pipelines，和加载数据时的 samplers 。
- **models 是最关键的部分，包括旋转检测模型和损失函数。**
- 在 apis 中，我们为模型训练、测试和推理提供一键启动的接口。
- core 中实现了用于**模型训练的评估工具**和**定制的 hooks** 。

另外，得益于 OpenMMLab 强大的且高度灵活的 config 模式和注册器机制， MMRotate 可以做到不改动代码**只编辑配置文件**便能自由切换不同的旋转框定义法。