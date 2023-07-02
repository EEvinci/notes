# mmdetection中模型配置文件的文件命名含义

## 以faster-rcnn为例

`faster-rcnn_r101-caffe_fpn_ms-3x_coco.py` 和 `faster-rcnn_r101_fpn_ms-3x_coco.py` 是两个不同的配置文件，它们用于设置 Faster R-CNN 目标检测算法的参数。文件名中的每个部分都代表着一种设置：

- `faster-rcnn`: 这代表使用的**目标检测算法是 Faster R-CNN**。
- `r101`: 这代表使用的 **`backbone 网络`**（即**用于特征提取的网络**）是 **ResNet-101**。
- `caffe`（只在第一个文件名中）: 这意味着**模型权重**是**从 Caffe 框架转换过来**的，而**不是 PyTorch 训练的**。
- `fpn`: 这代表使用了 **Feature Pyramid Network（FPN）**，FPN 是一种用于**提升小物体检测准确率**的特征提取方法。 
- `ms`: 这代表使用了多尺度训练策略。
- `3x`: 这表示训练周期的长度，`3x` 表示训练周期被乘以了3。
- `coco`: 这代表使用的数据集是 COCO 数据集。

两个配置文件的主要区别在于，`faster-rcnn_r101-caffe_fpn_ms-3x_coco.py` 使用的是从 Caffe 转换过来的模型权重，而 `faster-rcnn_r101_fpn_ms-3x_coco.py` 没有指明使用从其他框架转换过来的权重，可能直接是用 PyTorch 训练的权重。