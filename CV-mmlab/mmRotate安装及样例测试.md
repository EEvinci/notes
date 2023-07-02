# mmRotate安装及样例测试

首先在激活的conda环境中

**安装适合版本的Pytorch:**

```
conda install pytorch==1.8.0 torchvision==0.9.0 cudatoolkit=10.2 -c pytorch
```

下载mim:

```
pip install -U openmim
```

**从源码安装MMrotate:**

```
git clone https://github.com/open-mmlab/mmrotate.git
cd mmrotate
pip install -v -e .
```

**安装对应版本的mmcv full:**

![image-20230602234556268](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602234556268.png)

​	查看自己mmrotate版本:

​	![image-20230602234918679](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602234918679.png)

我们选择下对应版本的mmcv full:

![image-20230602235000052](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602235000052.png)

之后进行验证:

下载配置文件检查点文件:

```cmd
mim download mmrotate --config oriented_rcnn_r50_fpn_1x_dota_le90 --dest .
```

验证--输入以下代码,会在该目录下或者一个result.jpg的图片:

```python
python demo/image_demo.py demo/demo.jpg oriented_rcnn_r50_fpn_1x_dota_le90.py oriented_rcnn_r50_fpn_1x_dota_le90-6d2b2ce0.pth --out-file result.jpg
```

![image-20230602235310336](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230602235310336.png)
