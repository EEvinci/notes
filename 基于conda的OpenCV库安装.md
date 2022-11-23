# 基于conda的OpenCV库安装

## OpenCV库的调用名是`cv2`

所以会看到这样的import语句

```py
import cv2
```

这句话就是对openCV库的调用

## openCV库的下载安装

### First

好像不需要像网上的教程那样, 首先去官网下载exe执行文件, 然后在VS中进行配置

直接在teminal中, 进入要指定的conda环境, 然后输入`pip install opencv-python`即可

![image-20221123095326189](E:/Typora/ty_Photo/image-20221123095326189.png)

### 关于`WARNING: Ignoring invalid distribution`

进入括号中的地址，到site-packages中查找带前破折号的上述警告信息中所提到的破损的包，然后删除即可

![image-20221123095736480](E:/Typora/ty_Photo/image-20221123095736480.png)

### Second

可以采用whl下载方式

即在官网上先下载相应的whl包，然后在whl文件存放目录打开teminal，然后输入`pip install [whl包名]`, 进行安装

[openCV官网](https://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv)



## [参考文档](https://zhuanlan.zhihu.com/p/150124330)

