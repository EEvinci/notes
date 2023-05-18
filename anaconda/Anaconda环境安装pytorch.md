# Anaconda安装pytorch

```shell
//创建环境
conda create --name pytorch python==3.7

//查看已经创建的环境
conda info --env

//激活进入环境
conda actiavte pytorch

//然后就是通过pip来下载一些包

//进入pytorch的官网，用官方给出的命令行下载即可
//详见下方
```

[PyTorch官网](https://pytorch.org/)

我这次要下载的是pytorch1.10, 由于版本有些老旧, 所以进入previous versions中进行下载

![image-20221011154358185](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221011154358185.png)

进去之后会发现有conda文件和wheel文件两种下载方式

> [anaconda 搭建 pytorch 环境：conda 和 whl 两种方式](https://blog.csdn.net/pentiumCM/article/details/108859272)
>
> 重点看这篇文章的**方式二:whl**

选择wheel下载, 搭配豆瓣或者清华或者阿里镜像网站, 直接下载wheel文件, 速度较快

以pytorch1.10.1为例, 直接复制官网上的命令下载即可

## GPU加速

### 下载CUDA

安装适合的CUDA版本的GPU驱动程序和CUDA工具包, 从 NVIDIA 官方网站上下载

#### 以我的cuda版本为例

使用`nvcc --version`命令检查CUDA版本

![image-20230319235415998](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319235415998.png)

使用`nvidia-smi`查看GPU使用信息

![image-20230319235336178](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319235336178.png)

### 安装torch-gpu

[torch GPU cuda11.6安装]((https://blog.csdn.net/m0_61059963/article/details/127707293))

```cmd
pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

