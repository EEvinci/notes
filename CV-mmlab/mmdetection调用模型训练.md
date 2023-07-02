# mmdetection调用模型训练

[TOC]



## 转化数据集格式从labelme到coco

![image-20230612102840681](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612102840681.png)

## 首先data导进来

**以这样的形式命名**

![422f4e7e2cbcb305cbb44b92fa5d6af](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/422f4e7e2cbcb305cbb44b92fa5d6af.png)

因为现在mmdetection版本更新了到3.x

所以项目结构变了

## 改一下`coco.py`

![image-20230612004243817](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612004243817.png)

## 改一下`class_names.py`

![c8322758537f71481eaee4baa3672a7](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/c8322758537f71481eaee4baa3672a7.png)

## 在模型跑了之后看生成文件然后掐了

![5b472a88830c1b0bb8bcf346ab81681](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/5b472a88830c1b0bb8bcf346ab81681.png)

然后跑这个config

## 包版本

![068f69f2dcd16e5209241f387bbeb3f](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/068f69f2dcd16e5209241f387bbeb3f.png)

主要就是这三个包

mmdet好像要用mim安装

![f28a7b23695bdf6049be520d026d692](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/f28a7b23695bdf6049be520d026d692.png)

这包都是按官网教程装的

## 设置`PYTHONPATH`

```python
$env:PYTHONPATH += ";F:\Include\include\CV\openlab\mmdetection-3.x"
```

Python的`import`语句用于在当前模块中导入其他Python模块的代码。Python解释器会在一系列预定义的目录中查找要导入的模块，这些目录被称为Python路径（Python Path）。

当你执行一个Python脚本时，Python解释器会将当前脚本的目录自动添加到Python路径中。此外，Python还会在环境变量`PYTHONPATH`中指定的目录以及一些默认的位置（例如Python安装目录下的`Lib`和`site-packages`目录）中查找模块。

在你的情况下，错误信息提示Python解释器无法在Python路径中找到名为`projects.example_project.dummy`的模块。这可能是因为你的`projects`目录不在Python路径中。

要解决这个问题，你可以将包含`projects`目录的路径添加到`PYTHONPATH`环境变量中。例如，如果你的`projects`目录位于`F:\Include\include\CV\openlab\mmdetection-3.x`，你可以这样设置环境变量（在Windows命令提示符中）：

`$env:PYTHONPATH += ";F:\Include\include\CV\openlab\mmdetection-3.x"`

然后再次运行你的脚本，Python解释器就应该能够找到你的`projects.example_project.dummy`模块了。

注意，这种方法设置的环境变量只在当前的命令提示符会话中有效。如果你开启了新的命令提示符会话，你需要再次设置环境变量。如果你想让环境变量的设置在系统中持久保存，你需要将上述命令添加到你的系统环境变量设置中。

## diffustiondet模型

### 模型训练

![a7a2dad054ee09d263dcd817b9eed61](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/a7a2dad054ee09d263dcd817b9eed61.png)

![6d1356ac46f2929e1c610038127c297](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/6d1356ac46f2929e1c610038127c297.png)

这个估计要看轮数

我用这个模型跑了90000个

不知道效果咋样

因为一开始模型预设太高了450000

跑一分钟不到就爆了



### 跑完了

竟然因为一个图片不存在的错误而终止了

正好到15000个迭代

还好保存了一个checkpoint能够测试模型

![image-20230612084356693](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612084356693.png)

画个损失图

```python
python .\tools\analysis_tools\analyze_logs.py plot_curve .\Evinci\20230612_015115\vis_data\20230612_015115.json --keys loss loss_cls loss_bbox
```

可以加个输出路径`--out out.pdf`, 会输出到项目的根目录...

![image-20230612084614811](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612084614811.png)

![Figure_1](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/Figure_1.png)

### 检测模型

```python 
python tools/test.py Evinci_config\diffusiondet_r50_fpn_500-proposals_1-step_crop-ms-480-800-450k_coco.py Evinci_diffusiondet\iter_15000.pth --show
```

`--show`可以不加，这个过程是在验证集上进行训练，然后输出结果，加了`--show`会一张一张的显示，所以训练就特别慢

![image-20230612085524690](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612085524690.png)

如果不加，不到一分钟就出来结果了

![211029-019C_98_1_1129_312_0.717.png](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612204947239.png)

可以看到我模型里面标注的训练和测试集的训练log信息

![image-20230612205331605](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612205331605.png)

## yolo模型

第一次运行模型会下载一些文件

![image-20230612164126520](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612164126520.png)

一定是要在第一次启动之后然后掐掉, 运行的配置文件要从指定的工作目录中获取, 然后运行

可以在第一次运行之后把模型产生的配置文件放到自己的配置文件夹中, 然后修改一些必要的属性，再运行，这样基本上回没什么问题和bug

可以看到，模型下载完之后训练就开始正常运行了

![image-20230612164407110](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612164407110.png)

还有一个关键点，可以看到上述的loss非常大，因为没有加载预训练模型，所以模型是从头开始训练的，而自己的数据集图片总共就六七百张，数量还是很小的，所以想要早小数据集上有一个比较不错的效果，加载预训练模型是比较关键的

就是在`load_from`中填写预训练模型的路径，我是已经把要使用预训练模型的checkpoint文件都下载下来了

但是之后报了个奇怪的bug

## yolof模型

果然是就需要从自己的config配置文件进行启动

![image-20230612165330419](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230612165330419.png)

这样就成功了

虽然一开始肯定是要先从，configs下面的模型的配置文件运行

但是在`work-dir`生成配置文件之后，就要从该文件进行运行

但是之后报了个奇怪的bug



