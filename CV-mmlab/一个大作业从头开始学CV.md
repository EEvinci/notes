# 一个大作业从头开始学CV

## 因为选了最新的DiffusionDet模型...

选这个模型做了一个染色体目标检测的任务, 用`mmdetection`跑是跑出来了, 但是要讲解模型的基本原理, 所以要把之前的模型发展回顾了解一遍...不然感觉这个模型理解不了

因为`Diffusiondet`采用了`DETR`的思想, 也就是`detection transformer`, 所以就要知道`transformer`的工作原理, 然后再理解`DETR`

[transformer模型示意图](https://jalammar.github.io/images/t/transformer_decoding_2.gif)，真的好形象

![img](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/transformer_decoding_2.gif)

### 参考文档

[DETR](https://zhuanlan.zhihu.com/p/146065711) - 主要是他的参考文档

