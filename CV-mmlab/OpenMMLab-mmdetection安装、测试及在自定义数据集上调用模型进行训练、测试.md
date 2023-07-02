# OpenMMLab-mmdetection安装、测试及在自定义数据集上调用模型进行训练、测试

[toc]

## 创建conda环境

```cmd
conda create --name openmmlab python=3.8 -y
```

-y表示直接就是yes，不需要等到y/n出来, 直接一步到位

## 使用conda下载相关库文件

```cmd
conda install pytorch torchvision -c pytorch
```

> 在conda命令中，`-c`选项是用来指定要**从哪个channel安装包**。
>
> channel是**Anaconda分发的软件仓库**。这些channel可能包含不同版本的软件包或一些**在默认channel中找不到的软件包**。
>
> 在你给出的这个例子中，`-c pytorch`意味着conda将**从pytorch channel下载和安装pytorch和torchvision**。**这个channel是由PyTorch团队维护的，包含了他们发布的最新版本的PyTorch和相关的库。**

## 安装openmim - mim完全可以不用下

虽然安装了, 但是**每次用mim下载都会报retry,** 然后**再转回豆瓣源**, **等于没用mim**

```cmd
pip install -U openmim
```

![image-20230530225127412](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230530225127412.png)

## 安装mmcv

```cmd
 pip install "mmcv>=2.0.0"
```

![image-20230530225011388](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230530225011388.png)

## 安装mmdetection

```
pip install mmdet
```

## 不需要硬使用mim下载模型权重文件（如果遇到问题的话）

说的就是你这一步，让我烦的不行：

![image-20230602221737084](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602221737084.png)

就像这种文件`rtmdet_tiny_8xb32-300e_coco.py` 和 `rtmdet_tiny_8xb32-300e_coco_20220902_112414-78e30dcc.pth`

### 模型配置文件存放地

直接通过`clone源码`方式进行, 在clone源码后`.py`的**模型配置文件**都在源码根目录下的**`configs`**下的**各种模型文件夹**中, 如下

比如官网示例的`rtmdet`

![image-20230602222019159](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602222019159.png)

进去之后就是各种模型配置文件

![image-20230602222338430](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602222338430.png)

### 模型权重文件下载处

就在`configs`文件夹下、各个模型文件夹里面的`README`文件中

想用什么大小的模型直接点击链接下载即可

![image-20230602222323163](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602222323163.png)

然后**下载的模型权重文件**我放在了**根目录下的`checkpoints`文件夹**中`(这个是我自己创建的文件夹!!!)`

![image-20230602222643268](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602222643268.png)

## 运行示例

对一张图片进行目标检测

```python
python demo/image_demo.py demo/demo.jpg configs/rtmdet/rtmdet_tiny_8xb32-300e_coco.py --weights checkpoints/rtmdet_s_8xb32-300e_coco_20220905_161602-387a891e.pth 
```

`--device`后面可以使用gpu, 写`cuda:0`, 指定第一块gpu, 如果你用的是笔记本只有一块gpu的话

`device`默认就是第一块gpu，这个属性可以不写

但我这有问题

![image-20230602222954258](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602222954258.png)

### 输出文件

输出在根目录下的一个`outputs文件夹`文件夹中

![image-20230609145913996](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609145913996.png)

`outputs`中有两个文件夹, `preds`是存放`COCO`格式的图片, `vis`是存放`png`格式的图片

![image-20230609150113392](../AppData/Roaming/Typora/typora-user-images/image-20230609150113392.png)

![image-20230609150041835](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609150041835.png)

![image-20230609150141134](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609150141134.png)

我输出的图片很奇怪, 应该是模型调用的问题

![demo](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/demo.jpg)

## 用mmdetection调用模型在自己的数据集上进行目标检测

首先准备数据集

这里面像刚刚输出的图片一样, 有`png`格式和`COCO`格式的图片

![image-20230609150535673](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609150535673.png)

![image-20230609150614754](../AppData/Roaming/Typora/typora-user-images/image-20230609150614754.png)

![**image-20230609150643155**](../AppData/Roaming/Typora/typora-user-images/image-20230609150643155.png)

怎么调用`COCO`格式的数据?

怎么把这些数据全部放到模型中进行训练?

## COCO数据的理解

### 训练集

以下是我的COCO数据**`训练集`**的**树结构**:

有三个一级属性: 

- images:里面是图片的基本属性: `height` `width` `id` `file_name`(这个比较重要, 训练时会**根据图片名称从数据集指定路径中寻找图片进行调用**, 所以一定要确保**图片名称的正确**、以及图片名称**对应的图片是真实存在的**)
- categories: 包含了所有类别的信息，**每个类别有一个唯一的id和name**，还有一个**上级分类supercategory**（在某些情况下可能会使用，但**对于目标检测任务来说并非必须**）。
- `annotations`：包含了每个对象的**标注信息**，如`bbox`（**边界框，格式通常为[x_min, y_min, width, height]**），`category_id`（类别id），`image_id`（图片id），`area`（对象占据的面积），`segmentation`（对象的分割信息，**如果进行语义分割任务会用到**）等。

**看图片数量**直接看`images：`后面的**items数**

[JSON Editor Online](https://jsoneditoronline.org/) 使用这个网站对处理大量的JSON数据进行查看，可以将JSON数据**以树形结构展示**出来，使得结构一目了然

![image-20230609215834665](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609215834665.png)

![image-20230609215846156](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609215846156.png)

![image-20230609215859454](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609215859454.png)

![image-20230609215946098](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609215946098.png)

以上的数据是可以用于目标检测任务的，完全没有问题

因为对于目标检测任务，**最关键的信息就是`annotations属性中`的每个对象的`边界框（bbox）`和`类别（category_id）`**。而以上数据中，这些信息都是存在的。这样的数据格式**可以直接被很多目标检测的模型和库使用**，如Faster R-CNN，YOLO，SSD以及**MMDetection**等。

### 测试集



![image-20230609220215513](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609220215513.png)

里面的属性和训练集中的属性都是相同的

### png格式图片数量和COCO格式图片数量不一致

测试集中COCO格式的图片数量是67张，而png数量有96张；训练集也是两种格式图片数量不一样

只要`COCO中的图片都在png图片中，即COCO的json文件中写的图片名在png图片中都是真实存在的`，就没问题

![image-20230609223340346](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230609223340346.png)

- 对于**`MMDetection`**，**数据加载是以COCO格式的json文件为基准**。其中json文件的**`images`字段**会包含每张图片的基本信息，如**图片名`file_name`**，在进行训练和测试时，会根据你在**配置文件中填写的`img_prefix`路径与`file_name`进行拼接**，**从而找到具体的图片文件**。所以确实**需要你在配置文件中指明图片的路径**，以便于找到对应的图片文件。

- 对于**json中记录的图片数量<u>*少于*</u>实际png图片数量的情况**，一般情况下是不会引发错误的，MMDetection在加载数据时**主要依据的是json文件中的记录**，也就是说，**那些没有在json文件中记录的图片，在训练和测试过程中是不会被使用到的**。不过这里要注意，如果**json文件中包含了某张图片的信息**，但**实际上在对应的文件夹下并不存在这张图片**，这种情况下**就会引发错误**，因为在**加载数据时会尝试打开并读取这张图片**。所以，请**确保json文件中所有记录的图片都能在指定的文件夹下找到**。

## Faster-R-CNN中的名词理解

FCN分支是什么？全称说一下拜托然后再解释一下

> **FCN分支**：全称是**Fully Convolutional Network branch**。FCN是一种用于**图像语义分割**的神经网络，不同于普通的卷积神经网络，它**可以接收任意尺寸的输入图像**。在一些复杂的模型中，如Mask R-CNN，会使用**FCN**对**Roi Align后**的每一个**候选区域**做**像素级别的分割预测**，这就是FCN分支。

ROI-Pooling相比于平常的pooling其有什么不同？其pooling的过程是什么？

> **ROI-Pooling**：**Region of Interest Pooling**，是一种特殊的**池化方式**。在**传统的卷积神经网络**中，**pooling的窗口大小和步长是固定的**，但在ROI-Pooling中，**窗口的大小会根据输入的区域（ROI）的大小来确定**，目的是**将各种尺寸的ROI转化为固定大小的输出**，以便后续进行**分类**或者**bounding box回归**等操作。

Anchor在计算机视觉中指的是什么？anchor-based是一种什么方法？

> **Anchor**：Anchor在物体检测中通常是**预设的一组具有不同尺寸和宽高比的矩形框**，这些框用于以**滑动窗口**的方式在特征图上**生成候选区域**。Anchor-based方法则是一类**使用Anchor来生成候选区域的方法**，比如Faster R-CNN中的RPN网络就是典型的anchor-based方法。

RPN网络是什么？全称说一下拜托然后再解释一下

> **RPN网络**：RPN全称是**Region Proposal Network**，**区域提议网络**。这是Faster R-CNN中的一个重要组成部分，负责**生成候选区域**。RPN通过**在每个位置使用预设的Anchor**，对每个Anchor进行物体**存在性分类**和**bounding box回归**，从而生成一系列的候选区域。

DETR 是什么？全称说一下拜托然后再解释一下

> **DETR**：DETR全称是**DEtection TRansformer**。它是一种**新的目标检测方法**，**摒弃了传统的anchor-based方法**，而是**直接使用Transformer模型**来进行**目标检测**。DETR的输出是一组预测的**物体类别和bounding box**，这些输出是通过对输入图像的**全局视角**进行推理得到的。

box 具体指检测物体的检测框？

> **box**：在目标检测中，box通常指的是**bounding box（包围框）**，是用来标记图像中物体位置的矩形框，一般由框的**左上角**和**右下角**的坐标或者**框的中心坐标和宽高**来表示。

progressive refinement 是什么？在什么过程中用到的一种方法？

> **progressive refinement**：**渐进式优化**或渐进式精炼，是一种在训练过程中**逐步改进模型预测结果**的方法。这种方法在许多计算机视觉任务中都有应用，如**物体检测**、**语义分割**等。在物体检测中，经常会**在模型的预测结果上进行多次bounding box回归**，每次都**微调预测的bounding box**，以**逐步改进预测的精度**，这就是一种progressive refinement。

bounding box回归是什么?

> **Bounding box回归**：在**目标检测**中，通常我们的目标**不仅是识别图像中的物体类别**，还包括**确定物体的具体位置**。这个位置通常**由一个矩形框来表示**，也就是所谓的"bounding box"。而**"回归"在这里就是预测这个矩形框的过程**。更具体的说，是预测这个矩形框的**中心位置以及其宽度和高度**。这个过程需要训练模型学习到从**图像特征**到**矩形框大小和位置的映射关系**，这就是"bounding box回归"。

Roi Align是什么?

> **RoI Align**：在一些目标检测算法中，比如Faster R-CNN，我们需要从整张图像中**提取出一些小的、感兴趣的区域**，并对这些区域进行**进一步的处理。**这些小区域可能形状各异，大小不一，但是我们的**网络通常需要固定大小的输入**，这就需要我们对这些区域进行一些调整。RoI Align就是用于解决这个问题的一种技术，**它能保证从图像中提取出来的小区域，在经过处理后，不管原来的大小如何，输出都是一个固定大小的特征图**。

anchor的具体表现形式是什么?

> **Anchor**：在物体检测任务中，我们经常需要在图像中寻找**可能存在物体的位置**。一个常见的做法是，在图像中**划分很多小的格子**，然后在每个格子的位置预设一些大小和形状各异的矩形框，这些**预设的矩形框就叫做"anchor"**。在寻找物体时，我们就**检查每个anchor，看看是否有物体存在**。这样，anchor就提供了一种结构化的方式来在图像中寻找物体
