# Linux基于thundersvm使用GPU对svm进行加速

[TOC]

## 下载方法

[thundersvm—github](https://github.com/Xtra-Computing/thundersvm)

### pip快速下载

使用`pip install`快速下载方式只适用于Linux的`CUDA 9.0`的情况

#### 命令

`pip install thundersvm` 或 `pip install thundersvm-cu90-0.2.0-py3-none-linux_x86_64.whl`

该wheel文件可以从thundersvm的GitHub上进行获取

![image-20230629131036943](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629131036943.png)

如果Linux的**cuda版本不是9.0**那么要使用下面的**普通下载方式**

### 普通下载

普通下载是通过**git clone原项目然后在项目中进行构建的方式**进行

#### 命令

```shell
git clone https://github.com/Xtra-Computing/thundersvm.git
```

进入项目，**构建cmake**

```shell
cd thundersvm
mkdir build && cd build && cmake .. && make -j
```

#### 问题

最常见的问题应该是关于 `libthundersvm.so`的问题

在执行上述`build`和`make j`构建的过程中还可能会遇到一些包缺失**（比如cmake和libcurl3）**的问题

在我的情况下使用`apt install`安装`cmake`是会出现问题的，所以使用了**snap**

#### 解决方法

##### 以下操作需要使用sudo权限

首先安装**libcurl3**

`sudo apt install libcurl3`

![image-20230629132446588](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629132446588.png)

使用 `sudo snap install cmake --classic` 进行**cmake的下载**

![image-20230629132532388](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629132532388.png)

进入**thundersvm**下**刚刚创建的`build`目录**，执行 `sudo make install`进行cmake的构建

![image-20230629131837783](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629131837783.png)

然后在程序的执行路径中导入thundersvm的路径，就可以使用了

具体使用方法如下

## 使用thundersvm

我使用的是thundersvm中的SVC函数

进入thundersvm项目根目录，会发现其下有一个python目录，这就是python下thundersvm的源码存放位置，要调用的thundersvm中的函数也都在这里实现

而我们要做的也就是调用该python脚本中函数

![image-20230629132922133](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629132922133.png)

可以看到thundersvm除了支持python之外还支持MATLAB和R语言，根据语言的函数调用方式可以进行调用然后使用GPU进行加速，实现的都是svm算法

![image-20230629133011969](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629133011969.png)

![image-20230629133020407](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629133020407.png)

接下来就是在程序中调用python目录下thundersvm目录中的thundersvm脚本

![image-20230629133225019](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629133225019.png)

### 调用方式

在代码中使用**sys库引入该文件的执行路径**（按道理来说cmake构建好了之后thundersvm就会添加到程序的执行路径中，然后直接import thundersvm就可以使用了，但是我在使用的时候没有识别到）

```python
import sys
sys.path.append("thundersvm脚本的路径（建议使用绝对路径，省心）")
```

![image-20230629133454243](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629133454243.png)

将该执行路径添加之后，可以使用查看该程序中的执行路径

```python
print(sys.path)
```

![image-20230629133653410](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629133653410.png)

可以看到我再进行cmake构建之后，thundersvm的执行路径并没有被检测到，所以需要手动添加

添加之后就可以引入thundersvm库，如果import成功即可以使用，即大功告成

```python
import thundersvm
或
from thundersvm import SVC
```

这两个都一样

![image-20230629133913446](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629133913446.png)

看到可以使用之后就成功了,之后可以调用该库中的函数

## 在代码中的使用

### 训练代码更改

在代码中的使用非常简单, 只需要替换掉原先使用的svm函数即可

例如我要是用SVC函数进行模型的训练

之前的定义如下

```python
from sklearn import svm
...
svc = svm.SVC(max_iter=96000, verbose=True)
```

#### 更改内容

现在的定义如下

```python
from thundersvm import SVC
...
svc = SVC(max_iter=96000, verbose=True)
```

即可

### 加载模型同样需要导入thundersvm

在使用joblib库对模型导出, 要放到混淆矩阵中进行模型性能评估时

例如如下过程将模型放到混淆矩阵中进行指标评测

```python
import joblib

joblib.dump(model, "model.joblib") # 这里的.joblib后缀可以不加,即使不加导出的文件的类型也不会变化,但是加了可以增加识别度,让人一看就能看出来这是一个模型文件

model = joblib.load('model.joblib')

# 混淆矩阵
conf_mat = confusion_matrix(list(y_test), list(y_pred), labels=labels)

accuracy = accuracy_score(y_test, y_pred)
precision= precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1_score = f1_score(y_test, y_pred)
```

如果该模型是使用thundersvm训练出来的, 那么**在加载的时候也需要thundersvm**

因为 **ThunderSVM 使用了自己的模型格式和内部实现**，与其他 SVM 库（如 scikit-learn）的模型格式**不兼容**, 在加载模型时，**需要使用 ThunderSVM 库**来**解析和还原模型的参数**以及使用相应的算法进行预测。

#### 更改内容

所以上述代码应该**添加thundersvm的库引入**, **只需添加如下代码:**

```python
import sys
sys.path.append("thundersvm/python/thundersvm") #这里根据自己的路径进行更改

from thundersvm import SVC
...
```

即可