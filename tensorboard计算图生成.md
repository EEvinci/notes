### tensorboard计算图生成

- 先输入代码：

```python
writer=tf.summary.FileWriter(r"D:TensorBoardData", tf.get_default_graph())
writer.close()
```

其中`D:TensorBoardData`,  是要存放计算图的位置

- 然后在终端中进入conda环境

再输入

```cmd
tensorboard --logdir=D:TensorBoardData
```

此时会显示一个地址

点击这个地址, 就可以看到tensorboard的计算图

![image-20221026094108538](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221026094108538.png)

