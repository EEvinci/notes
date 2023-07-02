# thundersvm源码查看学习

[toc]

## 评估器(Estimator)和辅助类(Mixin)

在库引入部分, 看到`thundersvm`从`sklearn.base`中继承了两个类

![image-20230629150025202](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629150025202.png)

一个是`BaseEstimator`评估器基类, 另一个是`Mixin`辅助类

在 scikit-learn 中，**评估器是实现机器学习算法的对象**，用于**对数据进行拟合和预测**。例如，线性回归模型、决策树分类器等都是评估器。

Mixin是一种用于**在类中混合（mix-in）功能**的技术, 这里**只引入了两种Mixin**: `RegressionMixin`和`ClassfierMixin`, 即回归任务和分类任务

这两个 mixin 类提供的主要功能如下：

1. `RegressorMixin` 提供了**回归任务**中常用的方法和属性，例如 **`fit`**（拟合模型）、**`predict`**（进行预测）、**`score`**（计算模型的性能得分）等。
2. `ClassifierMixin` 提供了**分类任务中**常用的方法和属性，例如 `fit`、`predict`、`score`，以及其他一些分类特定的方法，如 **`predict_proba`（返回样本属于每个类别的概率）**、**`decision_function`（返回样本的决策函数值）**等。



在评估器`sklearn.base`的源码中, 可以看到如下函数

![image-20230629150102997](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629150102997.png)

关于`BaseEstimator`基本上都是一些**参数的获取和设置相关的函数**, 即BaseEstimator主要实现的就是参数的传入和设置相关功能

![image-20230629151232600](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629151232600.png)

关于**Mixin**有多种类型, 其主要实现的就是模型训练和评估等相关功能

### 问题

那么在最开始的介绍中说, 评估器用于对数据进行拟合和预测, 但是看到源码其实现的都是一些参数传递设置相关的函数

- 那么在评估器中拟合和预测是怎么进行的呢? 
- 而Mixin中主要实现了模型的训练和评估等函数, 其和Mixin辅助类之间的关系是什么?
- 其具体的组合和调用方式是什么?

### 理解

很明显,**评估器会调用辅助类中的函数**. 

评估器类通常会定义一些通用的方法，如参数传入和返回的函数，但**不会直接定义具体的训练和评估函数**。相反，评估器类会利用继承的辅助类来实现具体的训练和评估功能。



也就是说`sklearn.base`中**函数构建的思想**基于以下几点： 

- 将**参数传入设置等基础函数**和**训练中的函数**的定义分隔开, 因为训练任务类型较多, 所以对每一中训练类型进行相关的函数定义, 然后在具体的训练函数调用中进行实现
- 将**参数传入设置等基础函数**作为评估器的**主体部分**作为baseEstimator
- 在具体的Estimator中**继承BaseEstimator**中的变量和函数定义, 用于**实现具体的训练细节**
- 对于不同类别的训练任务，考虑到**所需要的功能不统一, 有些任务需要特定的函数**, 所以**定义不同类别的Mixin基类**

在具体的任务中，例如svm, 肯定要构建svm的评估器, 该评估器继承BaseEstimator，然后根据svm训练的任务类型调用相应的Mixin辅助类进行模型的训练和评估

而且thundersvm也正是这样的实现方式

![image-20230629153235999](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629153235999.png)

对其进行命名之后在svm模型中继承ThundersvmBase也就是BaseEstimator

![image-20230629153414339](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629153414339.png)

![image-20230629153424272](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629153424272.png)

然后传入参数和实现相关的函数

## OS验证识别

![image-20230629154153669](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230629154153669.png)

可以看到Thundersvm对于**Windows**、**Linux**和**Mac**都是支持的

**darwin指的是达尔文即Mac OS**，和Windows没有关系

## 函数实现

![image-20230630085928474](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230630085928474.png)

其只对SvmModel进行了详细的实现, 对于其他的算法均采用继承SvmModel的方式, 并根据算法和相对应的任务类型添加Mixin辅助类的继承

## 挖个坑 - 考完研把里面的具体实现研究一下