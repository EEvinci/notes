Anaconda环境安装pytorch

```cmd
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

![image-20221011154358185](E:\Typora\ty_Photo\image-20221011154358185.png)

进去之后会发现有conda文件和wheel文件两种下载方式

> [anaconda 搭建 pytorch 环境：conda 和 whl 两种方式](https://blog.csdn.net/pentiumCM/article/details/108859272)
>
> 重点看这篇文章的**方式二:whl**

选择wheel下载, 搭配豆瓣或者清华或者阿里镜像网站, 直接下载wheel文件, 速度较快

以pytorch1.10.1为例, 直接复制官网上的命令下载即可