# AutoGluon初体验

[TOC]



## AutoGluon_Background

Autogluon的发明人是李沐（Mu Li）和他在亚利桑那州立大学的研究团队。

Autogluon是一种**自动化机器学习工具**, 可以同时支持两种模式：**迁移学习模式**和**自动机器学习模式**。

如果你**已经训练好了一个模型**，并且想在**新的数据集**上进行迁移学习，则可以使用Autogluon的**迁移学习模式**。在这种模式下，你可以将预先训练好的模型作为初始模型，然后**使用新的数据集进行微调**。Autogluon提供了API，可以将预训练的模型加载到迁移学习框架中，并进行微调和优化。

如果没有预训练的模型，想**自动化地训练一个新的模型**，则可以使用Autogluon的**自动机器学习模式**。在这种模式下，你只需要**提供数据集**，并**指定一些基本的参数**，Autogluon将**自动执行整个机器学习过程**，包括**数据预处理、特征选择、模型选择**和**调整**，从而为你生成一个**最佳**的模型。

Autogluon可以自动生成的模型任务类型包括:

1. 二分类任务（Binary classification）：根据输入数据预测两个类别之一。
2. 多分类任务（Multiclass classification）：根据输入数据预测多个类别之一。
3. 回归任务（Regression）：根据输入数据预测数值型输出。
4. 时间序列任务（Time series forecasting）：根据时间序列数据预测未来的趋势和趋势变化。
5. 推荐任务（Recommendation）：根据用户行为历史和其他信息预测用户可能感兴趣的内容或商品。
6. 图像分类任务（Image classification）：根据输入的图像数据对图像进行分类。
7. 自然语言处理任务（Natural language processing）：根据输入的文本数据对文本进行分类或者生成。
8. 异常检测任务（Anomaly detection）：根据输入的数据检测异常或者离群点。

## AutoGluon安装

截至目前(2023.3.19), autoGluon现在最新的版本是0.7.0, 要求python最新的版本是3.8, 也可以是3.9或3.10

![image-20230319014858449](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319014858449.png)

使用`pip install autogluon`进行安装.

在这之前最好使用anaconda对python环境进行管理, 并且在一个**指定的环境**中进行autogluon的安装

install过程中会安装**大量的机器学习包**, 安装过程有些**缓慢**, 是我安装的时间最长的一个包

![image-20230319014811720](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319014811720.png)



## 运行示例

```python
# First install package from terminal:
# pip install -U pip
# pip install -U setuptools wheel
# pip install autogluon  # autogluon==0.7.0

from autogluon.tabular import TabularDataset, TabularPredictor
train_data = TabularDataset('https://autogluon.s3.amazonaws.com/datasets/Inc/train.csv')
test_data = TabularDataset('https://autogluon.s3.amazonaws.com/datasets/Inc/test.csv')
predictor = TabularPredictor(label='class').fit(train_data, time_limit=120)  # Fit models for 120s
leaderboard = predictor.leaderboard(test_data)
```

**PS: 以下的所有输出都是aotuGluon的功能输出**

### 打印相关配置信息

![image-20230319024601193](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319024601193.png)

### 数据预处理过程

![image-20230319024635312](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319024635312.png)

### 特征工程

![image-20230319024729075](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319024729075.png)

### 模型训练

显示**最优模型**及**各个模型的训练精度**

![image-20230319024939442](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230319024939442.png)

## NLP模型训练

要训练NLP任务, 就要用到`autogluon.text`包, 但是这个包不包含在`autogluon`包中

所以安装过`autogluon`包之后还要再安装`autogluon.text`这个包, 其中又有很多已经安装过的机器学习的包的重新安装

> 

### 使用模型

Autogluon在进行文本分类任务时，会自动尝试使用多种模型，并根据数据的特点和性质自适应地选择最佳的模型。常用的模型包括：

1. 词袋模型（Bag of Words）
2. TF-IDF 模型
3. FastText 模型
4. BERT 模型
5. RoBERTa 模型
6. DistilBERT 模型
7. ALBERT 模型
8. XLNet 模型

Autogluon会自动进行模型超参数搜索和选择，以获得最佳的模型性能。



Autogluon在处理NLP任务时常用的模型：

1. Bag-of-words (BoW) 模型：将文本转换为固定长度的向量表示，常用于文本分类等任务。

2. 词袋模型加上n-gram特征： 在BoW模型的基础上，将相邻的n个词组成一个特征，增加了上下文信息，提高了模型性能。

3. TF-IDF模型：在BoW的基础上，考虑了词频和文档频率，减小了一些常见但无关紧要的词对模型的影响。

4. 词嵌入模型：将词映射为低维向量，保留了词之间的语义关系，常用于句子相似度、情感分析等任务。常见的词嵌入模型包括 Word2vec、GloVe 和 fastText 等。

5. 卷积神经网络（CNN）模型：对于文本数据，可以将其看做一个1维信号，利用CNN提取特征，在文本分类和情感分析等任务中有良好的表现。

6. 循环神经网络（RNN）模型：通过对历史输入进行迭代计算，可以自然地处理变长的序列数据，包括语言模型、机器翻译等任务。常见的RNN模型包括LSTM和GRU。

7. 注意力机制（Attention）模型：通过动态地对输入进行加权，能够更好地捕捉文本中的关键信息，提高了模型的表现，在文本分类和情感分析等任务中有良好的表现。常见的注意力模型包括 Transformer 和 BERT。

   

chatGPT说的, 估计瞎扯了不少

## AutoGluon模块功能

AutoGluon 被模块化为专门用于表格、文本或图像数据的子模块。您可以通过单独安装特定子模块来减少所需的依赖项数量：python3 -m pip install <submodule>，其中 <submodule>可能是以下选项之一：

- autogluon.tabular - 仅用于表格数据 (TabularPredictor)
- autogluon.tabular独立的默认安装是一个骨架安装。
- 通过 pip install autogluon.tabular[all]安装与通过 pip install autogluon安装相同
- 可用的可选依赖项：lightgbm、catboost、xgboost、fastai。这些都包括在内。
- 实验性可选依赖项：skex。这将使 KNN 模型在 CPU 上的训练和推理速度提高 25 倍。使用 pip install autogluon.tabular[all,skex]启用，或在标准安装 AutoGluon 后 pip install “scikit-learn-intelex<2021.3”
- autogluon.vision - 仅用于计算机视觉（ImagePredictor、ObjectDetector）
- autogluon.text - 仅用于自然语言处理 (TextPredictor)
- autogluon.core - 仅对任意代码/模型的超参数调整有用的核心功能（Searcher/Scheduler）。
- autogluon.features - 仅用于特征生成/特征预处理管道的功能（主要与表格数据相关）。
- autogluon.extra - 各种额外功能，例如Efficient Neural Architecture Search
- autogluon.mxnet - MXNet 的杂项额外功能。

## GPU加速

- 安装 CUDA

  安装适合的CUDA版本的GPU驱动程序和CUDA工具包, 从 NVIDIA 官方网站上下载

  安装完成后，使用`nvcc --version`命令检查CUDA版本

  使用`nvidia-smi`查看GPU使用信息

- [torch GPU cuda11.6安装]([win11配置torch GPU环境（cuda 11.6 or 11.3）_torch环境_小四01的博客-CSDN博客](https://blog.csdn.net/m0_61059963/article/details/127707293))

  ```cmd
  pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113 -i https://pypi.tuna.tsinghua.edu.cn/simple
  ```

  很有效

## 包安装过程信息

## 参考文档

[AutoGluon GPU 版本 安装配置教程](https://blog.csdn.net/fyfugoyfa/article/details/125442923)

[AutoML for Image, Text, Time Series, and Tabular Data](https://github.com/autogluon/autogluon)

[Windows 上安装和使用 AutoGluon v0.4](https://www.youtube.com/watch?v=TsAxNgVogO0)

[AutoGluon官网](https://auto.gluon.ai/stable/index.html)

[autogluon 0.7.0-pypi](https://pypi.org/project/autogluon/)

## 包安装过程信息

### autogluon过程

以下是安装的**包的版本信息**, 留作参考

使用`Ctrl+F`，对特定包**版本**进行搜索

> Collecting autogluon
> Downloading http://pypi.doubanio.com/packages/d7/0d/8a748a529ec0deca693234a948c8e7cff3f3f1ebeb2d5bccc8f330be00da/autogluon-0.7.0-py3-none-any.whl (9.7 kB)
> Collecting autogluon.tabular[all]==0.7.0
> Downloading http://pypi.doubanio.com/packages/81/3e/59c74cb2d2978baacb0975c889230f156e07ea92aceb1f2154eb436d7a4b/autogluon.tabular-0.7.0-py3-none-any.whl (292 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 292.2/292.2 kB 2.3 MB/s eta 0:00:00
> Collecting autogluon.multimodal==0.7.0
> Downloading http://pypi.doubanio.com/packages/5a/be/2e2c29811c1ef265d50cd571b93ca2c0d1314dc6ebf42b50875a81a90e0c/autogluon.multimodal-0.7.0-py3-none-any.whl (331 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 331.1/331.1 kB 662.9 kB/s eta 0:00:00
> Collecting autogluon.core[all]==0.7.0
> Downloading http://pypi.doubanio.com/packages/94/7e/189df90f1c8287325e14655911c2e98f0f04eb9ca960f15665af84722ec1/autogluon.core-0.7.0-py3-none-any.whl (218 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 218.3/218.3 kB 2.2 MB/s eta 0:00:00
> Collecting autogluon.timeseries[all]==0.7.0
> Downloading http://pypi.doubanio.com/packages/5e/a4/abf483d6f5ea62fbbf8a780b19ac28b5343ff84b99609676658f8103560f/autogluon.timeseries-0.7.0-py3-none-any.whl (108 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 108.7/108.7 kB 3.2 MB/s eta 0:00:00
> Collecting autogluon.features==0.7.0
> Downloading http://pypi.doubanio.com/packages/3a/d7/fd1e6c37249a43299bf4eea6ec7482debe736045246b76466c3072d960c1/autogluon.features-0.7.0-py3-none-any.whl (60 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.1/60.1 kB 3.1 MB/s eta 0:00:00
> Requirement already satisfied: requests in e:\anaconda\envs\autog\lib\site-packages (from autogluon.core[all]==0.7.0->autogluon) (2.18.4)
> Collecting pandas<1.6,>=1.4.1
> Downloading http://pypi.doubanio.com/packages/ca/4e/d18db7d5ff9d28264cd2a7e2499b8701108f0e6c698e382cfd5d20685c21/pandas-1.5.3-cp38-cp38-win_amd64.whl (11.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.0/11.0 MB 4.8 MB/s eta 0:00:00
> Collecting scikit-learn<1.3,>=1.0
> Downloading http://pypi.doubanio.com/packages/5b/fb/478a0460ae2843dd2fc7a7f9ddcd8bb033ae21eb968df6a8cbe8094a28bc/scikit_learn-1.2.2-cp38-cp38-win_amd64.whl (8.3 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.3/8.3 MB 6.2 MB/s eta 0:00:00
> Collecting scipy<1.12,>=1.5.4
> Downloading http://pypi.doubanio.com/packages/32/8e/7f403535ddf826348c9b8417791e28712019962f7e90ff845896d6325d09/scipy-1.10.1-cp38-cp38-win_amd64.whl (42.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.2/42.2 MB 8.4 MB/s eta 0:00:00
> Collecting numpy<1.27,>=1.21
> Downloading http://pypi.doubanio.com/packages/bf/8c/3d36cef521739bd481e9a5b30e5c0f9faf8b7fe7b904238368908a9d149d/numpy-1.24.2-cp38-cp38-win_amd64.whl (14.9 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.9/14.9 MB 8.2 MB/s eta 0:00:00
> Collecting matplotlib
> Downloading http://pypi.doubanio.com/packages/92/01/2c04d328db6955d77f8f60c17068dde8aa66f153b2c599ca03c2cb0d5567/matplotlib-3.7.1-cp38-cp38-win_amd64.whl (7.6 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.6/7.6 MB 4.5 MB/s eta 0:00:00
> Collecting networkx<3.0,>=2.3
> Downloading http://pypi.doubanio.com/packages/42/31/d2f89f1ae42718f8c8a9e440ebe38d7d5fe1e0d9eb9178ce779e365b3ab0/networkx-2.8.8-py3-none-any.whl (2.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 4.3 MB/s eta 0:00:00
> Collecting boto3<2,>=1.10
> Downloading http://pypi.doubanio.com/packages/eb/cb/f1a65f2dbc9b64eeb7952e67a78430e365cfa578c1221dbec26e0587d054/boto3-1.26.92-py3-none-any.whl (134 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 134.7/134.7 kB 4.0 MB/s eta 0:00:00
> Collecting autogluon.common==0.7.0
> Downloading http://pypi.doubanio.com/packages/82/c4/91beb10ae79a4e20917f8c05ea49bf3e8ac344efa9fa4581edac5586f062/autogluon.common-0.7.0-py3-none-any.whl (45 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.0/45.0 kB ? eta 0:00:00
> Collecting tqdm<5,>=4.38
> Downloading http://pypi.doubanio.com/packages/e6/02/a2cff6306177ae6bc73bc0665065de51dfb3b9db7373e122e2735faf0d97/tqdm-4.65.0-py3-none-any.whl (77 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 77.1/77.1 kB 4.2 MB/s eta 0:00:00
> Collecting ray<2.3,>=2.2
> Downloading http://pypi.doubanio.com/packages/d3/9d/a8124e8911c725631650a5510f112352d6ed0e20d99a3995fdf5d18b7a74/ray-2.2.0-cp38-cp38-win_amd64.whl (20.8 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.8/20.8 MB 6.5 MB/s eta 0:00:00
> Collecting hyperopt<0.2.8,>=0.2.7
> Downloading http://pypi.doubanio.com/packages/b6/cd/5b3334d39276067f54618ce0d0b48ed69d91352fbf137468c7095170d0e5/hyperopt-0.2.7-py2.py3-none-any.whl (1.6 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 4.4 MB/s eta 0:00:00
> Collecting pytorch-metric-learning<2.0,>=1.3.0
> Downloading http://pypi.doubanio.com/packages/23/d9/1e352c0d5c3247bb06ef38de1f511bf989d126d6a1aeaf02f5e2ae3fe682/pytorch_metric_learning-1.7.3-py3-none-any.whl (112 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 112.2/112.2 kB 3.3 MB/s eta 0:00:00
> Collecting nptyping<2.5.0,>=1.4.4
> Downloading http://pypi.doubanio.com/packages/b2/c1/e6f8c5f28f9b3bdb5c9c1d349a51941a30f90347b82bd5594363e81cf3ff/nptyping-2.4.1-py3-none-any.whl (36 kB)
> Collecting requests
> Downloading http://pypi.doubanio.com/packages/d2/f4/274d1dbe96b41cf4e0efb70cbced278ffd61b5c7bb70338b62af94ccb25b/requests-2.28.2-py3-none-any.whl (62 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.8/62.8 kB 3.3 MB/s eta 0:00:00
> Collecting pytesseract<0.3.11,>=0.3.9
> Downloading http://pypi.doubanio.com/packages/c5/54/ec007336f38d2d4ce61f3544af3e6855dacbf04a1ac8294f10cabe81146f/pytesseract-0.3.10-py3-none-any.whl (14 kB)
> Collecting tensorboard<3,>=2.9
> Downloading http://pypi.doubanio.com/packages/8d/71/75fcfab1ff98e3fad240f760d3a6b5ca6bdbcc5ed141fb7abd35cf63134c/tensorboard-2.12.0-py3-none-any.whl (5.6 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.6/5.6 MB 5.2 MB/s eta 0:00:00
> Collecting jinja2<3.2,>=3.0.3
> Downloading http://pypi.doubanio.com/packages/bc/c3/f068337a370801f372f2f8f6bad74a5c140f6fda3d9de154052708dd3c65/Jinja2-3.1.2-py3-none-any.whl (133 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 133.1/133.1 kB 2.0 MB/s eta 0:00:00
> Collecting defusedxml<0.7.2,>=0.7.1
> Downloading http://pypi.doubanio.com/packages/07/6c/aa3f2f849e01cb6a001cd8554a88d4c77c5c1a31c95bdf1cf9301e6d9ef4/defusedxml-0.7.1-py2.py3-none-any.whl (25 kB)
> Collecting evaluate<0.4.0,>=0.2.2
> Downloading http://pypi.doubanio.com/packages/53/1e/9390692b3583467d13caad4caf10f379d23e40314091f9e7018fbfd07126/evaluate-0.3.0-py3-none-any.whl (72 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 72.9/72.9 kB 2.0 MB/s eta 0:00:00
> Collecting text-unidecode<1.4,>=1.3
> Downloading http://pypi.doubanio.com/packages/a6/a5/c0b6468d3824fe3fde30dbb5e1f687b291608f9473681bbf7dabbf5a87d7/text_unidecode-1.3-py2.py3-none-any.whl (78 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.2/78.2 kB 2.2 MB/s eta 0:00:00
> Collecting jsonschema<4.18,>=4.14
> Downloading http://pypi.doubanio.com/packages/c1/97/c698bd9350f307daad79dd740806e1a59becd693bd11443a0f531e3229b3/jsonschema-4.17.3-py3-none-any.whl (90 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 90.4/90.4 kB 1.7 MB/s eta 0:00:00
> Collecting nltk<4.0.0,>=3.4.5
> Downloading http://pypi.doubanio.com/packages/a6/0a/0d20d2c0f16be91b9fa32a77b76c60f9baf6eba419e5ef5deca17af9c582/nltk-3.8.1-py3-none-any.whl (1.5 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.5/1.5 MB 3.3 MB/s eta 0:00:00
> Collecting scikit-image<0.20.0,>=0.19.1
> Downloading http://pypi.doubanio.com/packages/a1/13/c0fa403e7972ed505680f3e7a4ff64b16bca106175c7f2b9e2b00114d580/scikit_image-0.19.3-cp38-cp38-win_amd64.whl (12.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.2/12.2 MB 6.8 MB/s eta 0:00:00
> Collecting timm<0.7.0,>=0.6.12
> Downloading http://pypi.doubanio.com/packages/89/4e/97622efc48a6e0c11781ed8a3472c679f2c8a5cf6ebd58a57b050e758bfe/timm-0.6.12-py3-none-any.whl (549 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 549.1/549.1 kB 5.7 MB/s eta 0:00:00
> Collecting nlpaug<1.2.0,>=1.1.10
> Downloading http://pypi.doubanio.com/packages/1c/28/a799de8b713e7cf84214d48739d0343505ff0967f85055b82d65894e1d02/nlpaug-1.1.11-py3-none-any.whl (410 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 410.5/410.5 kB 2.5 MB/s eta 0:00:00
> Collecting seqeval<1.3.0,>=1.2.2
> Using cached seqeval-1.2.2-py3-none-any.whl
> Collecting sentencepiece<0.2.0,>=0.1.95
> Downloading http://pypi.doubanio.com/packages/72/31/92d0ada03abf4d2b98fdaa64f10d760225ac2a9a398c0fd7ba6f3660b17b/sentencepiece-0.1.97-cp38-cp38-win_amd64.whl (1.1 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 4.0 MB/s eta 0:00:00
> Collecting omegaconf<2.3.0,>=2.1.1
> Downloading http://pypi.doubanio.com/packages/98/c3/f00dcd6935c11555db6ad55bdada58706120974cacf9a861a7b948ea0619/omegaconf-2.2.3-py3-none-any.whl (79 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 79.3/79.3 kB 2.2 MB/s eta 0:00:00
> Collecting accelerate<0.17,>=0.9
> Downloading http://pypi.doubanio.com/packages/dc/0c/f95215bc5f65e0a5fb97d4febce7c18420002a4c3ea5182294dc576f17fb/accelerate-0.16.0-py3-none-any.whl (199 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 199.7/199.7 kB 2.4 MB/s eta 0:00:00
> Collecting transformers<4.27.0,>=4.23.0
> Downloading http://pypi.doubanio.com/packages/1e/e2/60c3f4691b16d126ee9cfe28f598b13c424b60350ab339aba81aef054b8f/transformers-4.26.1-py3-none-any.whl (6.3 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.3/6.3 MB 5.4 MB/s eta 0:00:00
> Collecting torchmetrics<0.9.0,>=0.8.0
> Downloading http://pypi.doubanio.com/packages/5b/bd/4d55ca67c0dfc79b882fd5175da35f9cee359a173776c85f1ecadb7e9d84/torchmetrics-0.8.2-py3-none-any.whl (409 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 409.8/409.8 kB 3.6 MB/s eta 0:00:00
> Collecting openmim<0.4.0,>0.1.5
> Downloading http://pypi.doubanio.com/packages/ef/2f/dc7ce077629d1234f9cf7f17896cdcd49be0791da99aea673cced49b9700/openmim-0.3.6-py2.py3-none-any.whl (51 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 51.3/51.3 kB ? eta 0:00:00
> Collecting pytorch-lightning<1.10.0,>=1.9.0
> Downloading http://pypi.doubanio.com/packages/ce/ac/09980114432e759e56e8ff35c16d05dd7c8c0f512c9a88a91c5110272a1f/pytorch_lightning-1.9.4-py3-none-any.whl (827 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 827.8/827.8 kB 3.5 MB/s eta 0:00:00
> Collecting Pillow<9.6,>=9.3
> Downloading http://pypi.doubanio.com/packages/8c/a3/f096c4199c0af6d205a9cf1f3440581614016d9cfcab3a4091ecd5d1e26b/Pillow-9.4.0-cp38-cp38-win_amd64.whl (2.5 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.5/2.5 MB 5.3 MB/s eta 0:00:00
> `Collecting torch<1.14,>=1.9
> Downloading http://pypi.doubanio.com/packages/a6/41/122f37c99422566ea74b9cce90eb9218f5e8fb2582466da220f95842a0a0/torch-1.13.1-cp38-cp38-win_amd64.whl (162.6 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 162.6/162.6 MB 8.6 MB/s eta 0:00:00`
> Collecting torchvision<0.15.0
> Downloading http://pypi.doubanio.com/packages/3a/e6/b631892eca70acccd4b86b1dcee4fd23347293e6a231de72af3eb464b1a0/torchvision-0.14.1-cp38-cp38-win_amd64.whl (1.1 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 4.6 MB/s eta 0:00:00
> Collecting fairscale<0.4.14,>=0.4.5
> Using cached fairscale-0.4.13-py3-none-any.whl
> Collecting lightgbm<3.4,>=3.3
> Downloading http://pypi.doubanio.com/packages/6a/31/13f80e5abac627c53375c1dc49404d622d929272a231c05b2f4f7bb98b9e/lightgbm-3.3.5-py3-none-win_amd64.whl (1.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.0/1.0 MB 5.0 MB/s eta 0:00:00
> Collecting catboost<1.2,>=1.0
> Downloading http://pypi.doubanio.com/packages/b9/e0/f900892a81ed348df69a4fa08cb9d489eb82c63a81ccce1fd908b65c06d5/catboost-1.1.1-cp38-none-win_amd64.whl (74.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 74.0/74.0 MB 9.9 MB/s eta 0:00:00
> Collecting fastai<2.8,>=2.3.1
> Downloading http://pypi.doubanio.com/packages/ae/c0/02fbce28fd5af5996d737ee1b801bbfc0866e89c3a253896eb516e6fe847/fastai-2.7.11-py3-none-any.whl (232 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 232.8/232.8 kB 3.6 MB/s eta 0:00:00
> Collecting xgboost<1.8,>=1.6
> Downloading http://pypi.doubanio.com/packages/f0/27/ab284de6d960a2a0f9002b49f928ba079991bdc63c607a95937f7de8fc12/xgboost-1.7.4-py3-none-win_amd64.whl (89.1 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 89.1/89.1 MB 10.9 MB/s eta 0:00:00
> Collecting joblib<2,>=1.1
> Downloading http://pypi.doubanio.com/packages/91/d4/3b4c8e5a30604df4c7518c562d4bf0502f2fa29221459226e140cf846512/joblib-1.2.0-py3-none-any.whl (297 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 298.0/298.0 kB 6.1 MB/s eta 0:00:00
> Collecting gluonts<0.13,>=0.12.0
> Downloading http://pypi.doubanio.com/packages/1c/5a/f3abd0c8c0bdf39cd51e91c832d4a706886b490ef301eff77c6e78d69d7a/gluonts-0.12.4-py3-none-any.whl (1.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.2/1.2 MB 3.7 MB/s eta 0:00:00
> Collecting statsmodels<0.14,>=0.13.0
> Downloading http://pypi.doubanio.com/packages/bf/1a/3bfedcdf9d042b85fadb434346ee203139d1deb3cf52196bfd4c932b4f5b/statsmodels-0.13.5-cp38-cp38-win_amd64.whl (9.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.2/9.2 MB 5.1 MB/s eta 0:00:00
> Collecting ujson<6,>=5
> Downloading http://pypi.doubanio.com/packages/1f/b5/2717793593172454fa7cfd61ca523bca71c9839ea6651b3d37260ef1b225/ujson-5.7.0-cp38-cp38-win_amd64.whl (41 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 41.4/41.4 kB 1.9 MB/s eta 0:00:00
> Collecting statsforecast<1.5,>=1.4.0
> Downloading http://pypi.doubanio.com/packages/f3/c0/919650a54c12434b5166d7ef16db6a8d8c303bff2b8c74119f1ee30fdc3c/statsforecast-1.4.0-py3-none-any.whl (91 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 92.0/92.0 kB 2.6 MB/s eta 0:00:00
> Collecting pmdarima<1.9,>=1.8.2
> Downloading http://pypi.doubanio.com/packages/38/17/c4ece62a2b8d590c8c598aad602fc64fc4079690c36b120db19feb861e8c/pmdarima-1.8.5-cp38-cp38-win_amd64.whl (602 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 602.3/602.3 kB 4.7 MB/s eta 0:00:00
> Collecting tbats<2,>=1.1
> Downloading http://pypi.doubanio.com/packages/30/71/7a75656e705070ef84f12fac79d2596badb9254f9c3ea8be24e872fa1dfa/tbats-1.1.2-py3-none-any.whl (43 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 43.8/43.8 kB 2.1 MB/s eta 0:00:00
> Collecting sktime<0.16,>=0.14
> Downloading http://pypi.doubanio.com/packages/dd/8c/1b5fd4ef1293e75c938e6a778fac9cbd1a81eef941b63674212bb8b2155a/sktime-0.15.1-py3-none-any.whl (16.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.0/16.0 MB 8.3 MB/s eta 0:00:00
> Collecting psutil<6,>=5.7.3
> Downloading http://pypi.doubanio.com/packages/25/6e/ba97809175c90cbdcd33b470e466ebf0854d15d1506e605cc0ddd284d5b6/psutil-5.9.4-cp36-abi3-win_amd64.whl (252 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 252.5/252.5 kB 1.9 MB/s eta 0:00:00
> Requirement already satisfied: setuptools in e:\anaconda\envs\autog\lib\site-packages (from autogluon.common==0.7.0->autogluon.core[all]==0.7.0->autogluon) (65.6.3)
> Collecting pyyaml
> Downloading http://pypi.doubanio.com/packages/a8/5b/c4d674846ea4b07ee239fbf6010bcc427c4e4552ba5655b446e36b9a40a7/PyYAML-6.0-cp38-cp38-win_amd64.whl (155 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 155.4/155.4 kB 9.7 MB/s eta 0:00:00
> Collecting packaging>=20.0
> Downloading http://pypi.doubanio.com/packages/ed/35/a31aed2993e398f6b09a790a181a7927eb14610ee8bbf02dc14d31677f1c/packaging-23.0-py3-none-any.whl (42 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.7/42.7 kB ? eta 0:00:00
> Collecting jmespath<2.0.0,>=0.7.1
> Downloading http://pypi.doubanio.com/packages/31/b4/b9b800c45527aadd64d5b442f9b932b00648617eb5d63d2c7a6587b7cafc/jmespath-1.0.1-py3-none-any.whl (20 kB)
> Collecting s3transfer<0.7.0,>=0.6.0
> Downloading http://pypi.doubanio.com/packages/5e/c6/af903b5fab3f9b5b1e883f49a770066314c6dcceb589cf938d48c89556c1/s3transfer-0.6.0-py3-none-any.whl (79 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 79.6/79.6 kB 2.2 MB/s eta 0:00:00
> Collecting botocore<1.30.0,>=1.29.92
> Downloading http://pypi.doubanio.com/packages/c7/fc/a3233f966da8df1a580a8e0e78e0be2adc57ad97c10aac303b15b7dbd0ac/botocore-1.29.94-py3-none-any.whl (10.5 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 10.5/10.5 MB 5.2 MB/s eta 0:00:00
> Collecting six
> Downloading http://pypi.doubanio.com/packages/d9/5a/e7c31adbe875f2abbb91bd84cf2dc52d792b5a01506781dbcf25c91daf11/six-1.16.0-py2.py3-none-any.whl (11 kB)
> Collecting graphviz
> Downloading http://pypi.doubanio.com/packages/de/5e/fcbb22c68208d39edff467809d06c9d81d7d27426460ebc598e55130c1aa/graphviz-0.20.1-py3-none-any.whl (47 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 47.0/47.0 kB ? eta 0:00:00
> Collecting plotly
> Downloading http://pypi.doubanio.com/packages/f7/f5/c5b30c0a6639f076615d56f628f507ae20388e8f8769aef99ce5ea2033c8/plotly-5.13.1-py2.py3-none-any.whl (15.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 15.2/15.2 MB 6.9 MB/s eta 0:00:00
> Collecting multiprocess
> Downloading http://pypi.doubanio.com/packages/13/95/8b875a678c6f9db81809dd5d6032e9f8628426e37f6aa6b7d404ba582de1/multiprocess-0.70.14-py38-none-any.whl (132 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 132.0/132.0 kB 3.9 MB/s eta 0:00:00
> Collecting datasets>=2.0.0
> Downloading http://pypi.doubanio.com/packages/fe/17/5825fdf034ff1a315becdbb9b6fe5a2bd9d8e724464535f18809593bf9c2/datasets-2.10.1-py3-none-any.whl (469 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 469.0/469.0 kB 3.7 MB/s eta 0:00:00
> Collecting fsspec[http]>=2021.05.0
> Downloading http://pypi.doubanio.com/packages/4f/65/887925f1549fcb6ac3abb23a747c10f5ab083e8471fe568768b18bdb15b2/fsspec-2023.3.0-py3-none-any.whl (145 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 145.4/145.4 kB 4.2 MB/s eta 0:00:00
> Collecting xxhash
> Downloading http://pypi.doubanio.com/packages/8f/9a/513e63de457bfd44ca942c783f519df82532b093564fd2b8744e2d13c667/xxhash-3.2.0-cp38-cp38-win_amd64.whl (30 kB)
> Collecting huggingface-hub>=0.7.0
> Downloading http://pypi.doubanio.com/packages/bf/59/1313190f66383772621727fe91955061505016805fd1f249e0763093760b/huggingface_hub-0.13.2-py3-none-any.whl (199 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 199.2/199.2 kB 2.4 MB/s eta 0:00:00
> Collecting dill
> Downloading http://pypi.doubanio.com/packages/be/e3/a84bf2e561beed15813080d693b4b27573262433fced9c1d1fea59e60553/dill-0.3.6-py3-none-any.whl (110 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 110.5/110.5 kB 3.1 MB/s eta 0:00:00
> Collecting responses<0.19
> Downloading http://pypi.doubanio.com/packages/79/f3/2b3a6dc5986303b3dd1bbbcf482022acb2583c428cd23f0b6d37b1a1a519/responses-0.18.0-py3-none-any.whl (38 kB)
> Collecting fastprogress>=0.2.4
> Downloading http://pypi.doubanio.com/packages/a7/8f/213223fdee199c55db81e2d0c669f30e8285c5be2526c4ed924de39247da/fastprogress-1.0.3-py3-none-any.whl (12 kB)
> Requirement already satisfied: pip in e:\anaconda\envs\autog\lib\site-packages (from fastai<2.8,>=2.3.1->autogluon.tabular[all]==0.7.0->autogluon) (23.0.1)
> Collecting fastcore<1.6,>=1.4.5
> Downloading http://pypi.doubanio.com/packages/51/88/488fc7f9a051e9681a7f9c0f89f20fcf58ab9413e8aa2f272c785179c872/fastcore-1.5.28-py3-none-any.whl (67 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 67.6/67.6 kB 3.6 MB/s eta 0:00:00
> Collecting fastdownload<2,>=0.0.5
> Downloading http://pypi.doubanio.com/packages/47/60/ed35253a05a70b63e4f52df1daa39a6a464a3e22b0bd060b77f63e2e2b6a/fastdownload-0.0.7-py3-none-any.whl (12 kB)
> Collecting spacy<4
> Downloading http://pypi.doubanio.com/packages/1b/c3/57efc89148b4ca7b37b329275fc66ba461d902e0d3a6801539b35de82f7d/spacy-3.5.1-cp38-cp38-win_amd64.whl (12.6 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.6/12.6 MB 7.2 MB/s eta 0:00:00
> Collecting typing-extensions~=4.0
> Downloading http://pypi.doubanio.com/packages/31/25/5abcd82372d3d4a3932e1fa8c3dbf9efac10cc7c0d16e78467460571b404/typing_extensions-4.5.0-py3-none-any.whl (27 kB)
> Collecting pydantic~=1.7
> Downloading http://pypi.doubanio.com/packages/0e/86/8a40e374bc2e93bb285e2589953781b909ad2260ff64c17012327c740282/pydantic-1.10.6-cp38-cp38-win_amd64.whl (2.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.2/2.2 MB 2.5 MB/s eta 0:00:00
> Collecting toolz~=0.10
> Downloading http://pypi.doubanio.com/packages/7f/5c/922a3508f5bda2892be3df86c74f9cf1e01217c2b1f8a0ac4841d903e3e9/toolz-0.12.0-py3-none-any.whl (55 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 55.8/55.8 kB 1.4 MB/s eta 0:00:00
> Collecting future
> Using cached future-0.18.3-py3-none-any.whl
> Collecting py4j
> Downloading http://pypi.doubanio.com/packages/10/30/a58b32568f1623aaad7db22aa9eafc4c6c194b429ff35bdc55ca2726da47/py4j-0.10.9.7-py2.py3-none-any.whl (200 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 200.5/200.5 kB 4.0 MB/s eta 0:00:00
> Collecting cloudpickle
> Downloading http://pypi.doubanio.com/packages/15/80/44286939ca215e88fa827b2aeb6fa3fd2b4a7af322485c7170d6f9fd96e0/cloudpickle-2.2.1-py3-none-any.whl (25 kB)
> Collecting MarkupSafe>=2.0
> Downloading http://pypi.doubanio.com/packages/93/fa/d72f68f84f8537ee8aa3e0764d1eb11e5e025a5ca90c16e94a40f894c2fc/MarkupSafe-2.1.2-cp38-cp38-win_amd64.whl (16 kB)
> Collecting importlib-resources>=1.4.0
> Downloading http://pypi.doubanio.com/packages/38/71/c13ea695a4393639830bf96baea956538ba7a9d06fcce7cef10bfff20f72/importlib_resources-5.12.0-py3-none-any.whl (36 kB)
> Collecting pyrsistent!=0.17.0,!=0.17.1,!=0.17.2,>=0.14.0
> Downloading http://pypi.doubanio.com/packages/b1/8d/bbce2d857ecdefb7170a8a37ade1de0f060052236c07693856ac23f3b1ee/pyrsistent-0.19.3-cp38-cp38-win_amd64.whl (62 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.7/62.7 kB 1.6 MB/s eta 0:00:00
> Collecting pkgutil-resolve-name>=1.3.10
> Downloading http://pypi.doubanio.com/packages/c9/5c/3d4882ba113fd55bdba9326c1e4c62a15e674a2501de4869e6bd6301f87e/pkgutil_resolve_name-1.3.10-py3-none-any.whl (4.7 kB)
> Collecting attrs>=17.4.0
> Downloading http://pypi.doubanio.com/packages/fb/6e/6f83bf616d2becdf333a1640f1d463fef3150e2e926b7010cb0f81c95e88/attrs-22.2.0-py3-none-any.whl (60 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.0/60.0 kB 1.6 MB/s eta 0:00:00
> Requirement already satisfied: wheel in e:\anaconda\envs\autog\lib\site-packages (from lightgbm<3.4,>=3.3->autogluon.tabular[all]==0.7.0->autogluon) (0.38.4)
> Collecting gdown>=4.0.0
> Downloading http://pypi.doubanio.com/packages/bc/c2/bf15a3e9a5551bc13d9fce0377376e6801fa4bd9fca964dc1ee093da2559/gdown-4.6.4-py3-none-any.whl (14 kB)
> Collecting click
> Downloading http://pypi.doubanio.com/packages/c2/f1/df59e28c642d583f7dacffb1e0965d0e00b218e0186d7858ac5233dce840/click-8.1.3-py3-none-any.whl (96 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.6/96.6 kB 2.8 MB/s eta 0:00:00
> Collecting regex>=2021.8.3
> Downloading http://pypi.doubanio.com/packages/1f/f3/895ba11bc0243becd38f8b7560d2e329c465ead247cfb815611c347d7fc1/regex-2022.10.31-cp38-cp38-win_amd64.whl (267 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 267.7/267.7 kB 2.7 MB/s eta 0:00:00
> Collecting antlr4-python3-runtime==4.9.*
> Using cached antlr4_python3_runtime-4.9.3-py3-none-any.whl
> Collecting rich
> Downloading http://pypi.doubanio.com/packages/6b/f0/79df8eaa345ece1d33d8dfeec46ea166028da37b314dc44ead18c058a126/rich-13.3.2-py3-none-any.whl (238 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 238.7/238.7 kB 3.7 MB/s eta 0:00:00
> Collecting colorama
> Downloading http://pypi.doubanio.com/packages/d1/d6/3965ed04c63042e047cb6a3e6ed1a63a35087b6a609aa3a15ed8ac56c221/colorama-0.4.6-py2.py3-none-any.whl (25 kB)
> Collecting model-index
> Downloading http://pypi.doubanio.com/packages/0f/a6/4d4cbbef704f186d143e2859296a610a355992e4eae71582bd598093b36a/model_index-0.1.11-py3-none-any.whl (34 kB)
> Collecting tabulate
> Downloading http://pypi.doubanio.com/packages/40/44/4a5f08c96eb108af5cb50b41f76142f0afa346dfa99d5296fe7202a11854/tabulate-0.9.0-py3-none-any.whl (35 kB)
> Collecting python-dateutil>=2.8.1
> Downloading http://pypi.doubanio.com/packages/36/7a/87837f39d0296e723bb9b62bbb257d0355c7f6128853c78955f57342a56d/python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 247.7/247.7 kB 2.2 MB/s eta 0:00:00
> Collecting pytz>=2020.1
> Downloading http://pypi.doubanio.com/packages/2e/09/fbd3c46dce130958ee8e0090f910f1fe39e502cc5ba0aadca1e8a2b932e5/pytz-2022.7.1-py2.py3-none-any.whl (499 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 499.4/499.4 kB 2.8 MB/s eta 0:00:00
> Requirement already satisfied: urllib3 in e:\anaconda\envs\autog\lib\site-packages (from pmdarima<1.9,>=1.8.2->autogluon.timeseries[all]==0.7.0->autogluon) (1.22)
> Collecting Cython!=0.29.18,>=0.29
> Downloading http://pypi.doubanio.com/packages/56/3a/e59db3769dee48409c759a88b62cd605324e05d396e10af0a065adc956ad/Cython-0.29.33-py2.py3-none-any.whl (987 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 987.3/987.3 kB 5.7 MB/s eta 0:00:00
> Collecting lightning-utilities>=0.6.0.post0
> Downloading http://pypi.doubanio.com/packages/5d/ec/a20c5d5f26894913da028110310ba55ee254e1b7ff0ff78441e4eeb7291f/lightning_utilities-0.8.0-py3-none-any.whl (20 kB)
> Collecting filelock
> Downloading http://pypi.doubanio.com/packages/9a/eb/95844b279593fd79c0a4d5eadad029203528509bccb0efe117543e1a1704/filelock-3.10.0-py3-none-any.whl (9.9 kB)
> Collecting virtualenv>=20.0.24
> Downloading http://pypi.doubanio.com/packages/86/2f/35a79942c38d4ca89b444085d67900f713f1967446fdcefc8351619d7c65/virtualenv-20.21.0-py3-none-any.whl (8.7 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.7/8.7 MB 7.8 MB/s eta 0:00:00
> Collecting protobuf!=3.19.5,>=3.15.3
> Downloading http://pypi.doubanio.com/packages/27/d2/68e09ac7a3771f2be6ef018f12da7ac38e470d9ce2ce011bc13861863715/protobuf-4.22.1-cp38-cp38-win_amd64.whl (420 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 420.6/420.6 kB 3.8 MB/s eta 0:00:00
> Collecting aiosignal
> Downloading http://pypi.doubanio.com/packages/76/ac/a7305707cb852b7e16ff80eaf5692309bde30e2b1100a1fcacdc8f731d97/aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
> Collecting frozenlist
> Downloading http://pypi.doubanio.com/packages/03/00/febbfd2ec244a0f91707bd879afe6aa278e337dc41cd9d0d25260e6da38e/frozenlist-1.3.3-cp38-cp38-win_amd64.whl (34 kB)
> Collecting grpcio>=1.32.0
> Downloading http://pypi.doubanio.com/packages/8d/0b/6b75908dac1028c0e7d070088e10951a3fe8f5ecc189ed12175526568a89/grpcio-1.51.3-cp38-cp38-win_amd64.whl (3.7 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.7/3.7 MB 6.1 MB/s eta 0:00:00
> Collecting msgpack<2.0.0,>=1.0.0
> Downloading http://pypi.doubanio.com/packages/da/46/855bdcbf004fd87b6a4451e8dcd61329439dcd9039887f71ca5085769216/msgpack-1.0.5-cp38-cp38-win_amd64.whl (62 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.5/62.5 kB 3.3 MB/s eta 0:00:00
> Collecting tensorboardX>=1.9
> Downloading http://pypi.doubanio.com/packages/60/9f/d532d37f10ac7af136d4c2ba71e1fe7af0f3cc0cc076dfc05826171e9737/tensorboardX-2.6-py2.py3-none-any.whl (114 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 114.5/114.5 kB 2.2 MB/s eta 0:00:00
> Requirement already satisfied: idna<4,>=2.5 in e:\anaconda\envs\autog\lib\site-packages (from requests->autogluon.core[all]==0.7.0->autogluon) (2.6)
> Requirement already satisfied: certifi>=2017.4.17 in e:\anaconda\envs\autog\lib\site-packages (from requests->autogluon.core[all]==0.7.0->autogluon) (2022.12.7)
> Collecting charset-normalizer<4,>=2
> Downloading http://pypi.doubanio.com/packages/26/20/83e1804a62b25891c4e770c94d9fd80233bbb3f2a51c4fadee7a196e5a5b/charset_normalizer-3.1.0-cp38-cp38-win_amd64.whl (96 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.4/96.4 kB 2.8 MB/s eta 0:00:00
> Collecting PyWavelets>=1.1.1
> Downloading http://pypi.doubanio.com/packages/a9/8f/f80ff31e73385b886c35fb9fb1377849f9c43a3c1195ed8dc8ed8dc1bd88/PyWavelets-1.4.1-cp38-cp38-win_amd64.whl (4.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.2/4.2 MB 6.3 MB/s eta 0:00:00
> Collecting tifffile>=2019.7.26
> Downloading http://pypi.doubanio.com/packages/87/4d/f4f4834ca37da0f1106fd0437f40931c91c26acba7d2db3535de5cb66649/tifffile-2023.3.15-py3-none-any.whl (218 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 218.6/218.6 kB 3.3 MB/s eta 0:00:00
> Collecting imageio>=2.4.1
> Downloading http://pypi.doubanio.com/packages/dc/0b/202efcb00ba89c749bb7b22634c917f29a58bdf052dabe8041f23743974f/imageio-2.26.0-py3-none-any.whl (3.4 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.4/3.4 MB 4.8 MB/s eta 0:00:00
> Collecting threadpoolctl>=2.0.0
> Downloading http://pypi.doubanio.com/packages/61/cf/6e354304bcb9c6413c4e02a747b600061c21d38ba51e7e544ac7bc66aecc/threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
> Collecting numba>=0.55
> Downloading http://pypi.doubanio.com/packages/22/6e/880d8ae26f26a3ecce71922797cc09b3b8a4e5274adecd0793f9b59d50b8/numba-0.56.4-cp38-cp38-win_amd64.whl (2.5 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.5/2.5 MB 3.1 MB/s eta 0:00:00
> Collecting deprecated>=1.2.13
> Downloading http://pypi.doubanio.com/packages/51/6a/c3a0408646408f7283b7bc550c30a32cc791181ec4618592eec13e066ce3/Deprecated-1.2.13-py2.py3-none-any.whl (9.6 kB)
> Collecting patsy>=0.5.2
> Downloading http://pypi.doubanio.com/packages/2a/e4/b3263b0e353f2be7b14f044d57874490c9cef1798a435f038683acea5c98/patsy-0.5.3-py2.py3-none-any.whl (233 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 233.8/233.8 kB 3.6 MB/s eta 0:00:00
> Collecting google-auth-oauthlib<0.5,>=0.4.1
> Downloading http://pypi.doubanio.com/packages/b1/0e/0636cc1448a7abc444fb1b3a63655e294e0d2d49092dc3de05241be6d43c/google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
> Collecting tensorboard-data-server<0.8.0,>=0.7.0
> Downloading http://pypi.doubanio.com/packages/9d/cc/6f07c0043b44b3c3879ecfec1b8a450b6f5e3f8dccfedc9f5f1bc2c650e6/tensorboard_data_server-0.7.0-py3-none-any.whl (2.4 kB)
> Collecting tensorboard-plugin-wit>=1.6.0
> Downloading http://pypi.doubanio.com/packages/e0/68/e8ecfac5dd594b676c23a7f07ea34c197d7d69b3313afdf8ac1b0a9905a2/tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 781.3/781.3 kB 4.1 MB/s eta 0:00:00
> Collecting markdown>=2.6.8
> Downloading http://pypi.doubanio.com/packages/86/be/ad281f7a3686b38dd8a307fa33210cdf2130404dfef668a37a4166d737ca/Markdown-3.4.1-py3-none-any.whl (93 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 93.3/93.3 kB 1.3 MB/s eta 0:00:00
> Collecting absl-py>=0.4
> Downloading http://pypi.doubanio.com/packages/dd/87/de5c32fa1b1c6c3305d576e299801d8655c175ca9557019906247b994331/absl_py-1.4.0-py3-none-any.whl (126 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 126.5/126.5 kB 2.5 MB/s eta 0:00:00
> Collecting google-auth<3,>=1.6.3
> Downloading http://pypi.doubanio.com/packages/93/c4/16f8ad44ed7544244a9883f35cc99dc96378652a0ec7cc39028b1c697a1e/google_auth-2.16.2-py2.py3-none-any.whl (177 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 177.2/177.2 kB 3.6 MB/s eta 0:00:00
> Collecting werkzeug>=1.0.1
> Downloading http://pypi.doubanio.com/packages/f6/f8/9da63c1617ae2a1dec2fbf6412f3a0cfe9d4ce029eccbda6e1e4258ca45f/Werkzeug-2.2.3-py3-none-any.whl (233 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 233.6/233.6 kB 2.9 MB/s eta 0:00:00
> Collecting pyDeprecate==0.3.*
> Downloading http://pypi.doubanio.com/packages/40/9c/173f3cf770e66f3c9592318806aebb8617ba405d6d4c09493dabea75985c/pyDeprecate-0.3.2-py3-none-any.whl (10 kB)
> Collecting tokenizers!=0.11.3,<0.14,>=0.11.1
> Downloading http://pypi.doubanio.com/packages/94/93/e459652043471e51337fb4837a973386ccd1ee6fc9104679ec4e5f8de11a/tokenizers-0.13.2-cp38-cp38-win_amd64.whl (3.3 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.3/3.3 MB 2.6 MB/s eta 0:00:00
> Collecting kiwisolver>=1.0.1
> Downloading http://pypi.doubanio.com/packages/4f/05/59b34e788bf2b45c7157c3d898d567d28bc42986c1b6772fb1af329eea0d/kiwisolver-1.4.4-cp38-cp38-win_amd64.whl (55 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 55.4/55.4 kB 2.8 MB/s eta 0:00:00
> Collecting fonttools>=4.22.0
> Downloading http://pypi.doubanio.com/packages/43/6e/810648a366d6488e1e0543f72dcb2016e54ec02933e302cd41d72599e90d/fonttools-4.39.0-py3-none-any.whl (1.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.0/1.0 MB 2.3 MB/s eta 0:00:00
> Collecting cycler>=0.10
> Downloading http://pypi.doubanio.com/packages/5c/f9/695d6bedebd747e5eb0fe8fad57b72fdf25411273a39791cde838d5a8f51/cycler-0.11.0-py3-none-any.whl (6.4 kB)
> Collecting pyparsing>=2.3.1
> Downloading http://pypi.doubanio.com/packages/6c/10/a7d0fa5baea8fe7b50f448ab742f26f52b80bfca85ac2be9d35cdd9a3246/pyparsing-3.0.9-py3-none-any.whl (98 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.3/98.3 kB 1.9 MB/s eta 0:00:00
> Collecting contourpy>=1.0.1
> Downloading http://pypi.doubanio.com/packages/08/ce/9bfe9f028cb5a8ee97898da52f4905e0e2d9ca8203ffdcdbe80e1769b549/contourpy-1.0.7-cp38-cp38-win_amd64.whl (162 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 163.0/163.0 kB 2.0 MB/s eta 0:00:00
> Collecting urllib3
> Downloading http://pypi.doubanio.com/packages/7b/f5/890a0baca17a61c1f92f72b81d3c31523c99bec609e60c292ea55b387ae8/urllib3-1.26.15-py2.py3-none-any.whl (140 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 140.9/140.9 kB 2.8 MB/s eta 0:00:00
> Collecting pyarrow>=6.0.0
> Downloading http://pypi.doubanio.com/packages/7b/04/96784be5122d322dc4d76de2d200cdaf02b72bcec6176687c64d0e2379dd/pyarrow-11.0.0-cp38-cp38-win_amd64.whl (20.6 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.6/20.6 MB 10.1 MB/s eta 0:00:00
> Collecting aiohttp
> Downloading http://pypi.doubanio.com/packages/48/5b/dabb02a8fe7da607c0b65d9086af36a2c77c509f3ee7efb7a80b008d7c7a/aiohttp-3.8.4-cp38-cp38-win_amd64.whl (324 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 324.5/324.5 kB 4.0 MB/s eta 0:00:00
> Collecting wrapt<2,>=1.10
> Downloading http://pypi.doubanio.com/packages/54/21/282abeb456f22d93533b2d373eeb393298a30b0cb0683fa8a4ed77654273/wrapt-1.15.0-cp38-cp38-win_amd64.whl (36 kB)
> Collecting beautifulsoup4
> Downloading http://pypi.doubanio.com/packages/c6/ee/16d6f808f5668317d7c23f942091fbc694bcded6aa39678e5167f61b2ba0/beautifulsoup4-4.11.2-py3-none-any.whl (129 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 129.4/129.4 kB 1.9 MB/s eta 0:00:00
> Collecting pyasn1-modules>=0.2.1
> Downloading http://pypi.doubanio.com/packages/95/de/214830a981892a3e286c3794f41ae67a4495df1108c3da8a9f62159b9a9d/pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 155.3/155.3 kB 4.7 MB/s eta 0:00:00
> Collecting cachetools<6.0,>=2.0.0
> Downloading http://pypi.doubanio.com/packages/db/14/2b48a834d349eee94677e8702ea2ef98b7c674b090153ea8d3f6a788584e/cachetools-5.3.0-py3-none-any.whl (9.3 kB)
> Collecting rsa<5,>=3.1.4
> Downloading http://pypi.doubanio.com/packages/49/97/fa78e3d2f65c02c8e1268b9aba606569fe97f6c8f7c2d74394553347c145/rsa-4.9-py3-none-any.whl (34 kB)
> Collecting requests-oauthlib>=0.7.0
> Downloading http://pypi.doubanio.com/packages/6f/bb/5deac77a9af870143c684ab46a7934038a53eb4aa975bc0687ed6ca2c610/requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
> Collecting zipp>=3.1.0
> Downloading http://pypi.doubanio.com/packages/5b/fa/c9e82bbe1af6266adf08afb563905eb87cab83fde00a0a08963510621047/zipp-3.15.0-py3-none-any.whl (6.8 kB)
> Collecting importlib-metadata>=4.4
> Downloading http://pypi.doubanio.com/packages/26/a7/9da7d5b23fc98ab3d424ac2c65613d63c1f401efb84ad50f2fa27b2caab4/importlib_metadata-6.0.0-py3-none-any.whl (21 kB)
> Collecting llvmlite<0.40,>=0.39.0dev0
> Downloading http://pypi.doubanio.com/packages/75/7f/9055977016e713a5c033c376a9ea9cb3d1092a02ee1421c41ccbcc5aa043/llvmlite-0.39.1-cp38-cp38-win_amd64.whl (23.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 23.2/23.2 MB 7.6 MB/s eta 0:00:00
> Collecting numpy<1.27,>=1.21
> Downloading http://pypi.doubanio.com/packages/4c/42/6274f92514fbefcb1caa66d56d82ac7ac89f7652c0cef1e159a4b79e09f1/numpy-1.23.5-cp38-cp38-win_amd64.whl (14.7 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.7/14.7 MB 10.6 MB/s eta 0:00:00
> Collecting thinc<8.2.0,>=8.1.8
> Downloading http://pypi.doubanio.com/packages/4a/66/6de436958cde4c706d3d18681651c25a2434363599cebe7807185adedcba/thinc-8.1.9-cp38-cp38-win_amd64.whl (1.5 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.5/1.5 MB 5.0 MB/s eta 0:00:00
> Collecting preshed<3.1.0,>=3.0.2
> Downloading http://pypi.doubanio.com/packages/74/a6/7a57125dcacea307af18bfaacc83003c388599cfbdff12b4f77f62e1fd0e/preshed-3.0.8-cp38-cp38-win_amd64.whl (96 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.7/96.7 kB 2.7 MB/s eta 0:00:00
> Collecting spacy-legacy<3.1.0,>=3.0.11
> Downloading http://pypi.doubanio.com/packages/c3/55/12e842c70ff8828e34e543a2c7176dac4da006ca6901c9e8b43efab8bc6b/spacy_legacy-3.0.12-py2.py3-none-any.whl (29 kB)
> Collecting catalogue<2.1.0,>=2.0.6
> Downloading http://pypi.doubanio.com/packages/dc/28/a2b0cc4bfa7916ef9caf08475be5810fc564411c5a801f225a1f40a458c5/catalogue-2.0.8-py3-none-any.whl (17 kB)
> Collecting wasabi<1.2.0,>=0.9.1
> Downloading http://pypi.doubanio.com/packages/58/5f/1f2833d59abf53e24dbadc21b0565fe10c64545da8705faed8eff3b14745/wasabi-1.1.1-py3-none-any.whl (27 kB)
> Collecting cymem<2.1.0,>=2.0.2
> Downloading http://pypi.doubanio.com/packages/96/99/a5f558006387913f1a1b4af5ccae610b19ebe5498e7199c2da10e77429c8/cymem-2.0.7-cp38-cp38-win_amd64.whl (30 kB)
> Collecting srsly<3.0.0,>=2.4.3
> Downloading http://pypi.doubanio.com/packages/75/18/7b25e88e7e7042d964554966838b36821ee7f95bddd397ce95e67d6ad5ba/srsly-2.4.6-cp38-cp38-win_amd64.whl (482 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 482.7/482.7 kB 2.7 MB/s eta 0:00:00
> Collecting murmurhash<1.1.0,>=0.28.0
> Downloading http://pypi.doubanio.com/packages/2c/16/a5223c2e02e6dd908fa0c93056f612ff6af6c639cbff631a380f45279beb/murmurhash-1.0.9-cp38-cp38-win_amd64.whl (18 kB)
> Collecting pathy>=0.10.0
> Downloading http://pypi.doubanio.com/packages/82/c6/683e3955de9a13b14dfa3ea358cd58f3914057e8064a2dcbfd450958e72e/pathy-0.10.1-py3-none-any.whl (48 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 48.9/48.9 kB ? eta 0:00:00
> Collecting smart-open<7.0.0,>=5.2.1
> Downloading http://pypi.doubanio.com/packages/47/80/c2d1bdd36c6b64ae566d9a29724291510e4f3796ce99639d3c2999286284/smart_open-6.3.0-py3-none-any.whl (56 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 56.8/56.8 kB 989.7 kB/s eta 0:00:00
> Collecting typer<0.8.0,>=0.3.0
> Downloading http://pypi.doubanio.com/packages/0d/44/56c3f48d2bb83d76f5c970aef8e2c3ebd6a832f09e3621c5395371fe6999/typer-0.7.0-py3-none-any.whl (38 kB)
> Collecting spacy-loggers<2.0.0,>=1.0.0
> Downloading http://pypi.doubanio.com/packages/62/8c/814e0bd139a8c94b50298be3a4e640d90cdce78efe0099e373a767b7d854/spacy_loggers-1.0.4-py3-none-any.whl (11 kB)
> Collecting langcodes<4.0.0,>=3.2.0
> Downloading http://pypi.doubanio.com/packages/fe/c3/0d04d248624a181e57c2870127dfa8d371973561caf54333c85e8f9133a2/langcodes-3.3.0-py3-none-any.whl (181 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.6/181.6 kB 2.2 MB/s eta 0:00:00
> Collecting protobuf!=3.19.5,>=3.15.3
> Downloading http://pypi.doubanio.com/packages/32/f8/52f598bceb16fe365f4ef8e957ac8890aeb56abf97d365ff5abd8c1250cf/protobuf-3.20.3-cp38-cp38-win_amd64.whl (904 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 904.4/904.4 kB 4.8 MB/s eta 0:00:00
> Collecting platformdirs<4,>=2.4
> Downloading http://pypi.doubanio.com/packages/7b/e1/593f693096c50411a2bf9571f66bc3be9d0f79a4a50e95aab581458b0e3c/platformdirs-3.1.1-py3-none-any.whl (14 kB)
> Collecting distlib<1,>=0.3.6
> Downloading http://pypi.doubanio.com/packages/76/cb/6bbd2b10170ed991cf64e8c8b85e01f2fb38f95d1bc77617569e0b0b26ac/distlib-0.3.6-py2.py3-none-any.whl (468 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 468.5/468.5 kB 5.8 MB/s eta 0:00:00
> Collecting ordered-set
> Downloading http://pypi.doubanio.com/packages/33/55/af02708f230eb77084a299d7b08175cff006dea4f2721074b92cdb0296c0/ordered_set-4.1.0-py3-none-any.whl (7.6 kB)
> Collecting tenacity>=6.2.0
> Downloading http://pypi.doubanio.com/packages/e7/b0/c23bd61e1b32c9b96fbca996c87784e196a812da8d621d8d04851f6c8181/tenacity-8.2.2-py3-none-any.whl (24 kB)
> Collecting markdown-it-py<3.0.0,>=2.2.0
> Downloading http://pypi.doubanio.com/packages/bf/25/2d88e8feee8e055d015343f9b86e370a1ccbec546f2865c98397aaef24af/markdown_it_py-2.2.0-py3-none-any.whl (84 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 84.5/84.5 kB 2.4 MB/s eta 0:00:00
> Collecting pygments<3.0.0,>=2.13.0
> Downloading http://pypi.doubanio.com/packages/0b/42/d9d95cc461f098f204cd20c85642ae40fbff81f74c300341b8d0e0df14e0/Pygments-2.14.0-py3-none-any.whl (1.1 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 4.0 MB/s eta 0:00:00
> Collecting multidict<7.0,>=4.5
> Downloading http://pypi.doubanio.com/packages/d2/cf/d00992d281fb953a01685d9b2e68f66901c7dee7bcb75dad1a5ef9a879d3/multidict-6.0.4-cp38-cp38-win_amd64.whl (28 kB)
> Collecting yarl<2.0,>=1.0
> Downloading http://pypi.doubanio.com/packages/f9/fa/9c746d29462714663d04cf9e34cc44a86efa17705a811c77556643b80f1b/yarl-1.8.2-cp38-cp38-win_amd64.whl (56 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 56.9/56.9 kB 3.1 MB/s eta 0:00:00
> Collecting async-timeout<5.0,>=4.0.0a3
> Downloading http://pypi.doubanio.com/packages/d6/c1/8991e7c5385b897b8c020cdaad718c5b087a6626d1d11a23e1ea87e325a7/async_timeout-4.0.2-py3-none-any.whl (5.8 kB)
> Collecting mdurl~=0.1
> Downloading http://pypi.doubanio.com/packages/b3/38/89ba8ad64ae25be8de66a6d463314cf1eb366222074cfda9ee839c56a4b4/mdurl-0.1.2-py3-none-any.whl (10.0 kB)
> Collecting pyasn1<0.5.0,>=0.4.6
> Downloading http://pypi.doubanio.com/packages/62/1e/a94a8d635fa3ce4cfc7f506003548d0a2447ae76fd5ca53932970fe3053f/pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 77.1/77.1 kB 4.5 MB/s eta 0:00:00
> Collecting oauthlib>=3.0.0
> Downloading http://pypi.doubanio.com/packages/7e/80/cab10959dc1faead58dc8384a781dfbf93cb4d33d50988f7a69f1b7c9bbe/oauthlib-3.2.2-py3-none-any.whl (151 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 151.7/151.7 kB 3.0 MB/s eta 0:00:00
> Collecting confection<1.0.0,>=0.0.1
> Downloading http://pypi.doubanio.com/packages/b1/c4/07291f4947d20f545eee76ef20d1eacfb1f80d1d6ab4792bfa6797e0578c/confection-0.0.4-py3-none-any.whl (32 kB)
> Collecting blis<0.8.0,>=0.7.8
> Downloading http://pypi.doubanio.com/packages/7c/36/eec5e1fd84c3078daa65823c6de8efbe5da3449dcfa763988c3afa232cbf/blis-0.7.9-cp38-cp38-win_amd64.whl (7.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.0/7.0 MB 932.1 kB/s eta 0:00:00
> Collecting soupsieve>1.2
> Downloading http://pypi.doubanio.com/packages/d2/70/2c92d7bc961ba43b7b21032b7622144de5f97dec14b62226533f6940798e/soupsieve-2.4-py3-none-any.whl (37 kB)
> Collecting PySocks!=1.5.7,>=1.5.6
> Downloading http://pypi.doubanio.com/packages/8d/59/b4572118e098ac8e46e399a1dd0f2d85403ce8bbaad9ec79373ed6badaf9/PySocks-1.7.1-py3-none-any.whl (16 kB)
> Installing collected packages: tokenizers, text-unidecode, tensorboard-plugin-wit, sentencepiece, pytz, pyasn1, py4j, msgpack, distlib, cymem, antlr4-python3-runtime, zipp, xxhash, wrapt, urllib3, ujson, typing-extensions, toolz, threadpoolctl, tensorboard-data-server, tenacity, tabulate, spacy-loggers, spacy-legacy, soupsieve, smart-open, six, rsa, regex, pyyaml, PySocks, pyrsistent, pyparsing, pygments, pyDeprecate, pyasn1-modules, psutil, protobuf, platformdirs, pkgutil-resolve-name, Pillow, packaging, ordered-set, oauthlib, numpy, networkx, murmurhash, multidict, mdurl, MarkupSafe, llvmlite, langcodes, kiwisolver, joblib, jmespath, grpcio, graphviz, future, fsspec, frozenlist, fonttools, filelock, fastprogress, dill, defusedxml, Cython, cycler, colorama, cloudpickle, charset-normalizer, catalogue, cachetools, attrs, async-timeout, absl-py, yarl, werkzeug, wasabi, virtualenv, tqdm, torch, tifffile, tensorboardX, srsly, scipy, requests, PyWavelets, python-dateutil, pytesseract, pydantic, pyarrow, preshed, plotly, patsy, omegaconf, nptyping, multiprocess, markdown-it-py, lightning-utilities, jinja2, importlib-resources, importlib-metadata, imageio, google-auth, fastcore, deprecated, contourpy, click, blis, beautifulsoup4, aiosignal, xgboost, typer, torchvision, torchmetrics, scikit-learn, scikit-image, rich, responses, requests-oauthlib, pandas, numba, nltk, matplotlib, markdown, jsonschema, hyperopt, huggingface-hub, fastdownload, fairscale, confection, botocore, aiohttp, accelerate, transformers, timm, thinc, statsmodels, seqeval, s3transfer, ray, pytorch-metric-learning, pathy, model-index, lightgbm, google-auth-oauthlib, gluonts, gdown, catboost, tensorboard, statsforecast, spacy, sktime, pytorch-lightning, pmdarima, openmim, nlpaug, datasets, boto3, tbats, fastai, evaluate, `autogluon.common, autogluon.features, autogluon.core, autogluon.tabular, autogluon.multimodal, autogluon.timeseries, autogluon`
> Attempting uninstall: urllib3
>  Found existing installation: urllib3 1.22
>  Uninstalling urllib3-1.22:
>    Successfully uninstalled urllib3-1.22
> Attempting uninstall: requests
>  Found existing installation: requests 2.18.4
>  Uninstalling requests-2.18.4:
>    Successfully uninstalled requests-2.18.4
> Successfully installed Cython-0.29.33 MarkupSafe-2.1.2 Pillow-9.4.0 PySocks-1.7.1 PyWavelets-1.4.1 absl-py-1.4.0 accelerate-0.16.0 aiohttp-3.8.4 aiosignal-1.3.1 antlr4-python3-runtime-4.9.3 async-timeout-4.0.2 attrs-22.2.0 `autogluon-0.7.0 autogluon.common-0.7.0 autogluon.core-0.7.0 autogluon.features-0.7.0 autogluon.multimodal-0.7.0 autogluon.tabular-0.7.0 autogluon.timeseries-0.7.0` beautifulsoup4-4.11.2 blis-0.7.9 boto3-1.26.92 botocore-1.29.94 cachetools-5.3.0 catalogue-2.0.8 catboost-1.1.1 charset-normalizer-3.1.0 click-8.1.3 cloudpickle-2.2.1 colorama-0.4.6 confection-0.0.4 contourpy-1.0.7 cycler-0.11.0 cymem-2.0.7 datasets-2.10.1 defusedxml-0.7.1 deprecated-1.2.13 dill-0.3.6 distlib-0.3.6 evaluate-0.3.0 fairscale-0.4.13 fastai-2.7.11 fastcore-1.5.28 fastdownload-0.0.7 fastprogress-1.0.3 filelock-3.10.0 fonttools-4.39.0 frozenlist-1.3.3 fsspec-2023.3.0 future-0.18.3 gdown-4.6.4 gluonts-0.12.4 google-auth-2.16.2 google-auth-oauthlib-0.4.6 graphviz-0.20.1 grpcio-1.51.3 huggingface-hub-0.13.2 hyperopt-0.2.7 imageio-2.26.0 importlib-metadata-6.0.0 importlib-resources-5.12.0 jinja2-3.1.2 jmespath-1.0.1 joblib-1.2.0 jsonschema-4.17.3 kiwisolver-1.4.4 langcodes-3.3.0 lightgbm-3.3.5 lightning-utilities-0.8.0 llvmlite-0.39.1 markdown-3.4.1 markdown-it-py-2.2.0 matplotlib-3.7.1 mdurl-0.1.2 model-index-0.1.11 msgpack-1.0.5 multidict-6.0.4 multiprocess-0.70.14 murmurhash-1.0.9 networkx-2.8.8 nlpaug-1.1.11 nltk-3.8.1 nptyping-2.4.1 numba-0.56.4 numpy-1.23.5 oauthlib-3.2.2 omegaconf-2.2.3 openmim-0.3.6 ordered-set-4.1.0 packaging-23.0 pandas-1.5.3 pathy-0.10.1 patsy-0.5.3 pkgutil-resolve-name-1.3.10 platformdirs-3.1.1 plotly-5.13.1 pmdarima-1.8.5 preshed-3.0.8 protobuf-3.20.3 psutil-5.9.4 py4j-0.10.9.7 pyDeprecate-0.3.2 pyarrow-11.0.0 pyasn1-0.4.8 pyasn1-modules-0.2.8 pydantic-1.10.6 pygments-2.14.0 pyparsing-3.0.9 pyrsistent-0.19.3 pytesseract-0.3.10 python-dateutil-2.8.2 pytorch-lightning-1.9.4 pytorch-metric-learning-1.7.3 pytz-2022.7.1 pyyaml-6.0 ray-2.2.0 regex-2022.10.31 requests-2.28.2 requests-oauthlib-1.3.1 responses-0.18.0 rich-13.3.2 rsa-4.9 s3transfer-0.6.0 scikit-image-0.19.3 scikit-learn-1.2.2 scipy-1.10.1 sentencepiece-0.1.97 seqeval-1.2.2 six-1.16.0 sktime-0.15.1 smart-open-6.3.0 soupsieve-2.4 spacy-3.5.1 spacy-legacy-3.0.12 spacy-loggers-1.0.4 srsly-2.4.6 statsforecast-1.4.0 statsmodels-0.13.5 tabulate-0.9.0 tbats-1.1.2 tenacity-8.2.2 tensorboard-2.12.0 tensorboard-data-server-0.7.0 tensorboard-plugin-wit-1.8.1 tensorboardX-2.6 text-unidecode-1.3 thinc-8.1.9 threadpoolctl-3.1.0 tifffile-2023.3.15 timm-0.6.12 tokenizers-0.13.2 toolz-0.12.0 **`torch-1.13.1`** torchmetrics-0.8.2 torchvision-0.14.1 tqdm-4.65.0 transformers-4.26.1 typer-0.7.0 typing-extensions-4.5.0 ujson-5.7.0 urllib3-1.26.15 virtualenv-20.21.0 wasabi-1.1.1 werkzeug-2.2.3 wrapt-1.15.0 xgboost-1.7.4 xxhash-3.2.0 yarl-1.8.2 zipp-3.15.0
>
> **PS: 如果之前没有安装过torch, 在安装过程中应该还会带有torch-gpu版本的安装, 我这里因为之前安装过了GPU的版本所以没有附带安装.**

在过程中并没有`mxnet`的安装

### autogluon.text过程

这真的是我安装过的最麻烦的模型库

其中还涉及到一大堆的库之间的适配问题

> (autog) PS C:\Users\PC> pip install autogluon.text
> Looking in indexes: http://pypi.douban.com/simple
> Collecting autogluon.text
> Downloading http://pypi.doubanio.com/packages/10/60/bbbd4f5e1bf879034209d65d194890c970a91b73f1666eb930c19a4fcd25/autogluon.text-0.6.2-py3-none-any.whl (62 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.1/62.1 kB 3.2 MB/s eta 0:00:00
> Collecting autogluon.multimodal==0.6.2
> Downloading http://pypi.doubanio.com/packages/1d/39/51afde293205e5987feafb0cef71d68e3a51ceff1dc629a09bfdf4145939/autogluon.multimodal-0.6.2-py3-none-any.whl (303 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 303.4/303.4 kB 2.7 MB/s eta 0:00:00
> Collecting pytorch-metric-learning<1.4.0,>=1.3.0
> Downloading http://pypi.doubanio.com/packages/50/e6/8ec6adb0d17f690958421603c4daebf1362ff2083270f769c8ce3c533809/pytorch_metric_learning-1.3.2-py3-none-any.whl (109 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 109.4/109.4 kB 2.1 MB/s eta 0:00:00
> Collecting jsonschema<=4.8.0
> Downloading http://pypi.doubanio.com/packages/51/6b/0de110de6223c7fb45dc5a7c0ad19208bcc6017ca8b6adad9aa12066eb83/jsonschema-4.8.0-py3-none-any.whl (81 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 81.4/81.4 kB 4.5 MB/s eta 0:00:00
> Collecting albumentations<=1.2.0,>=1.1.0
> Downloading http://pypi.doubanio.com/packages/70/15/cb9a2173255c44726ed8d0048a03bbe2b2c290d4dea51563e75de0ab5ea4/albumentations-1.2.0-py3-none-any.whl (113 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 113.5/113.5 kB 3.3 MB/s eta 0:00:00
> Collecting scikit-learn<1.2,>=1.0.0
> Downloading http://pypi.doubanio.com/packages/67/41/55197045c3ea6b443977eb0222a98b4f5276a3aae3856baa57f39fdfea8e/scikit_learn-1.1.3-cp38-cp38-win_amd64.whl (7.5 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.5/7.5 MB 3.3 MB/s eta 0:00:00
> Collecting omegaconf<2.2.0,>=2.1.1
> Downloading http://pypi.doubanio.com/packages/2f/ae/5fd6ba3e3ef122bc5acf51e58a0dce03c9aa90e69069993133aa190be768/omegaconf-2.1.2-py3-none-any.whl (74 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 74.7/74.7 kB 2.1 MB/s eta 0:00:00
> Collecting autogluon.features==0.6.2
> Downloading http://pypi.doubanio.com/packages/0e/ef/d1aeb94d1a83792de575b2d373cc6848d1e213c4097339af1383f3f15e79/autogluon.features-0.6.2-py3-none-any.whl (60 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.0/60.0 kB 3.1 MB/s eta 0:00:00
> Requirement already satisfied: nltk<4.0.0,>=3.4.5 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (3.8.1)
> Requirement already satisfied: Pillow<=9.4.0,>=9.3.0 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (9.4.0)
> Requirement already satisfied: text-unidecode<=1.3 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (1.3)
> Collecting autogluon.common==0.6.2
> Downloading http://pypi.doubanio.com/packages/3d/09/fda1ed03bd403b5df11c8a1dd428bd6aaceac407474fd9cbdd85750467df/autogluon.common-0.6.2-py3-none-any.whl (44 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 44.7/44.7 kB ? eta 0:00:00
> Requirement already satisfied: pandas!=1.4.0,<1.6,>=1.2.5 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (1.5.3)
> Requirement already satisfied: seqeval<=1.2.2 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (1.2.2)
> Requirement already satisfied: torchmetrics<0.9.0,>=0.8.0 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (0.8.2)
> Collecting nlpaug<=1.1.10,>=1.1.10
> Downloading http://pypi.doubanio.com/packages/d8/a8/03e049908a155822f7d8900d3e2161ad9b97917b79b4ba064c223c5b44d8/nlpaug-1.1.10-py3-none-any.whl (410 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 410.8/410.8 kB 3.7 MB/s eta 0:00:00
> Collecting torchtext<0.14.0
> Downloading http://pypi.doubanio.com/packages/e3/9e/0e1b780b0d60fb7672df1364efbf4755c9bbd6b18f70e0186dc8513121b7/torchtext-0.13.1-cp38-cp38-win_amd64.whl (2.2 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.2/2.2 MB 5.7 MB/s eta 0:00:00
> Collecting torch<1.13,>=1.9
> Downloading http://pypi.doubanio.com/packages/e7/ae/2e4166eae0a2693ad9233da1c927f5f1b4d050d9d906ba656e1771d7c852/torch-1.12.1-cp38-cp38-win_amd64.whl (161.9 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 161.9/161.9 MB 10.4 MB/s eta 0:00:00
> Collecting autogluon.core[raytune]==0.6.2
> Downloading http://pypi.doubanio.com/packages/31/e5/8881b3ba6f0c07d772fcec62a121451f967e5087d4c2a5d32b1d2f16b92f/autogluon.core-0.6.2-py3-none-any.whl (226 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 226.5/226.5 kB 3.4 MB/s eta 0:00:00
> Requirement already satisfied: tqdm>=4.38.0 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (4.65.0)
> Collecting smart-open<5.3.0,>=5.2.1
> Downloading http://pypi.doubanio.com/packages/cd/11/05f68ea934c24ade38e95ac30a38407767787c4e3db1776eae4886ad8c95/smart_open-5.2.1-py3-none-any.whl (58 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 58.6/58.6 kB 3.0 MB/s eta 0:00:00
> Requirement already satisfied: sentencepiece<0.2.0,>=0.1.95 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (0.1.97)
> Collecting nptyping<1.5.0,>=1.4.4
> Downloading http://pypi.doubanio.com/packages/8f/d9/0514384fbad1c269d861f1dfe8ef8adc9d8ccaac1fdaad9f007063b9d92f/nptyping-1.4.4-py3-none-any.whl (31 kB)
> Collecting fairscale<=0.4.6,>=0.4.5
> Downloading http://pypi.doubanio.com/packages/42/d8/4efb77f32ffc1f4480a5bb783d963da0dacac0c7ee2708b8d73a7e9f55ae/fairscale-0.4.6.tar.gz (248 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 248.2/248.2 kB 1.5 MB/s eta 0:00:00
> Installing build dependencies ... done
> Getting requirements to build wheel ... done
> Installing backend dependencies ... done
> Preparing metadata (pyproject.toml) ... done
> Requirement already satisfied: defusedxml<=0.7.1,>=0.7.1 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (0.7.1)
> Requirement already satisfied: numpy<1.24,>=1.21 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (1.23.5)
> Collecting accelerate<0.14,>=0.9
> Downloading http://pypi.doubanio.com/packages/a9/aa/3b0f4b0858ff7f0888291039fd306c3c4e96b91baf5cb9828fcdcb1129d1/accelerate-0.13.2-py3-none-any.whl (148 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 148.8/148.8 kB 2.2 MB/s eta 0:00:00
> Collecting openmim<=0.2.1,>0.1.5
> Downloading http://pypi.doubanio.com/packages/a5/da/e6910f4f8e15231823a9c29ecaf3d96184176a15e7d20b45283000147e69/openmim-0.2.1-py2.py3-none-any.whl (49 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 49.7/49.7 kB 1.2 MB/s eta 0:00:00
> Collecting pytorch-lightning<1.8.0,>=1.7.4
> Downloading http://pypi.doubanio.com/packages/00/eb/3b2152f9c3a50d265f3e75529254228ace8a86e9a4397f3004f1e3be7825/pytorch_lightning-1.7.7-py3-none-any.whl (708 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 708.1/708.1 kB 2.6 MB/s eta 0:00:00
> Requirement already satisfied: scikit-image<0.20.0,>=0.19.1 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (0.19.3)
> Requirement already satisfied: boto3 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (1.26.92)
> Requirement already satisfied: timm<0.7.0 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (0.6.12)
> Collecting torchvision<0.14.0
> Downloading http://pypi.doubanio.com/packages/48/77/736239716ceb9ed1d8bfb923d9bb9e6dfe6e5addd8bac80943981efde09e/torchvision-0.13.1-cp38-cp38-win_amd64.whl (1.1 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 4.2 MB/s eta 0:00:00
> Requirement already satisfied: requests in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (2.28.2)
> Collecting scipy<1.10.0,>=1.5.4
> Downloading http://pypi.doubanio.com/packages/42/14/d2500818b7bb7b862d70c1ae97e646a4795b068583c67720553764095024/scipy-1.9.3-cp38-cp38-win_amd64.whl (39.8 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 39.8/39.8 MB 10.4 MB/s eta 0:00:00
> Collecting transformers<4.24.0,>=4.23.0
> Downloading http://pypi.doubanio.com/packages/15/6d/ad50f2ccf677556bdce7dd6f3f91bcd74e5dc8c1d7e4df78e216dd807319/transformers-4.23.1-py3-none-any.whl (5.3 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.3/5.3 MB 2.3 MB/s eta 0:00:00
> Requirement already satisfied: evaluate<=0.3.0 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.multimodal==0.6.2->autogluon.text) (0.3.0)
> Requirement already satisfied: psutil<6,>=5.7.3 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.common==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (5.9.4)
> Requirement already satisfied: setuptools in e:\anaconda\envs\autog\lib\site-packages (from autogluon.common==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (65.6.3)
> Collecting distributed<=2021.11.2,>=2021.09.1
> Downloading http://pypi.doubanio.com/packages/52/18/0c619038754f474bb4ee42d854168d5ef029d055b0a93f222d874c47881b/distributed-2021.11.2-py3-none-any.whl (802 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 802.2/802.2 kB 3.0 MB/s eta 0:00:00
> Requirement already satisfied: networkx<3.0,>=2.3 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (2.8.8)
> Collecting dask<=2021.11.2,>=2021.09.1
> Downloading http://pypi.doubanio.com/packages/e8/3e/161fc6b630603ab69266c90238068793e5cdd38b5e41b0fcba3d09636f1d/dask-2021.11.2-py3-none-any.whl (1.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.0/1.0 MB 3.8 MB/s eta 0:00:00
> Requirement already satisfied: matplotlib in e:\anaconda\envs\autog\lib\site-packages (from autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (3.7.1)
> Collecting ray[tune]<2.1,>=2.0
> Downloading http://pypi.doubanio.com/packages/c4/8f/96715a2731e8b1d8ef561fb22477cb44961388010580e7db93ba59bc3a62/ray-2.0.1-cp38-cp38-win_amd64.whl (20.7 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.7/20.7 MB 8.3 MB/s eta 0:00:00
> Requirement already satisfied: hyperopt<0.2.8,>=0.2.7 in e:\anaconda\envs\autog\lib\site-packages (from autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (0.2.7)
> Requirement already satisfied: packaging>=20.0 in e:\anaconda\envs\autog\lib\site-packages (from accelerate<0.14,>=0.9->autogluon.multimodal==0.6.2->autogluon.text) (23.0)
> Requirement already satisfied: pyyaml in e:\anaconda\envs\autog\lib\site-packages (from accelerate<0.14,>=0.9->autogluon.multimodal==0.6.2->autogluon.text) (6.0)
> Collecting opencv-python-headless>=4.1.1
> Downloading http://pypi.doubanio.com/packages/31/4b/15d990b72661b70005ac0a63fb2da778391a503ab88e53f4d45949f898ed/opencv_python_headless-4.7.0.72-cp37-abi3-win_amd64.whl (38.1 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 38.1/38.1 MB 10.5 MB/s eta 0:00:00
> Collecting qudida>=0.0.4
> Downloading http://pypi.doubanio.com/packages/f0/a1/a5f4bebaa31d109003909809d88aeb0d4b201463a9ea29308d9e4f9e7655/qudida-0.0.4-py3-none-any.whl (3.5 kB)
> Collecting albumentations<=1.2.0,>=1.1.0
> Downloading http://pypi.doubanio.com/packages/75/27/a8b0a738f8423b7ef9d0c9f8e73d5867395dbdae563c1655e9548cf700b9/albumentations-1.1.0-py3-none-any.whl (102 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 102.4/102.4 kB 3.0 MB/s eta 0:00:00
> Requirement already satisfied: responses<0.19 in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (0.18.0)
> Requirement already satisfied: fsspec[http]>=2021.05.0 in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (2023.3.0)
> Requirement already satisfied: datasets>=2.0.0 in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (2.10.1)
> Requirement already satisfied: multiprocess in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (0.70.14)
> Requirement already satisfied: dill in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (0.3.6)
> Requirement already satisfied: huggingface-hub>=0.7.0 in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (0.13.2)
> Requirement already satisfied: xxhash in e:\anaconda\envs\autog\lib\site-packages (from evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (3.2.0)
> Requirement already satisfied: pyrsistent!=0.17.0,!=0.17.1,!=0.17.2,>=0.14.0 in e:\anaconda\envs\autog\lib\site-packages (from jsonschema<=4.8.0->autogluon.multimodal==0.6.2->autogluon.text) (0.19.3)
> Requirement already satisfied: importlib-resources>=1.4.0 in e:\anaconda\envs\autog\lib\site-packages (from jsonschema<=4.8.0->autogluon.multimodal==0.6.2->autogluon.text) (5.12.0)
> Requirement already satisfied: attrs>=17.4.0 in e:\anaconda\envs\autog\lib\site-packages (from jsonschema<=4.8.0->autogluon.multimodal==0.6.2->autogluon.text) (22.2.0)
> Requirement already satisfied: regex>=2021.8.3 in e:\anaconda\envs\autog\lib\site-packages (from nltk<4.0.0,>=3.4.5->autogluon.multimodal==0.6.2->autogluon.text) (2022.10.31)
> Requirement already satisfied: joblib in e:\anaconda\envs\autog\lib\site-packages (from nltk<4.0.0,>=3.4.5->autogluon.multimodal==0.6.2->autogluon.text) (1.2.0)
> Requirement already satisfied: click in e:\anaconda\envs\autog\lib\site-packages (from nltk<4.0.0,>=3.4.5->autogluon.multimodal==0.6.2->autogluon.text) (8.1.3)
> Collecting typish>=1.7.0
> Downloading http://pypi.doubanio.com/packages/9d/d6/3f56c9c0c12adf61dfcf4ed5c8ffd2c431db8dd85592067a57e8e1968565/typish-1.9.3-py3-none-any.whl (45 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.1/45.1 kB ? eta 0:00:00
> Collecting antlr4-python3-runtime==4.8
> Downloading http://pypi.doubanio.com/packages/56/02/789a0bddf9c9b31b14c3e79ec22b9656185a803dc31c15f006f9855ece0d/antlr4-python3-runtime-4.8.tar.gz (112 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 112.4/112.4 kB 2.2 MB/s eta 0:00:00
> Preparing metadata (setup.py) ... done
> Requirement already satisfied: pip>=19.3 in e:\anaconda\envs\autog\lib\site-packages (from openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (23.0.1)
> Requirement already satisfied: tabulate in e:\anaconda\envs\autog\lib\site-packages (from openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (0.9.0)
> Requirement already satisfied: model-index in e:\anaconda\envs\autog\lib\site-packages (from openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (0.1.11)
> Requirement already satisfied: colorama in e:\anaconda\envs\autog\lib\site-packages (from openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (0.4.6)
> Requirement already satisfied: rich in e:\anaconda\envs\autog\lib\site-packages (from openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (13.3.2)
> Requirement already satisfied: pytz>=2020.1 in e:\anaconda\envs\autog\lib\site-packages (from pandas!=1.4.0,<1.6,>=1.2.5->autogluon.multimodal==0.6.2->autogluon.text) (2022.7.1)
> Requirement already satisfied: python-dateutil>=2.8.1 in e:\anaconda\envs\autog\lib\site-packages (from pandas!=1.4.0,<1.6,>=1.2.5->autogluon.multimodal==0.6.2->autogluon.text) (2.8.2)
> Requirement already satisfied: typing-extensions>=4.0.0 in e:\anaconda\envs\autog\lib\site-packages (from pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (4.5.0)
> Requirement already satisfied: tensorboard>=2.9.1 in e:\anaconda\envs\autog\lib\site-packages (from pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (2.12.0)
> Requirement already satisfied: pyDeprecate>=0.3.1 in e:\anaconda\envs\autog\lib\site-packages (from pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (0.3.2)
> Requirement already satisfied: charset-normalizer<4,>=2 in e:\anaconda\envs\autog\lib\site-packages (from requests->autogluon.multimodal==0.6.2->autogluon.text) (3.1.0)
> Requirement already satisfied: certifi>=2017.4.17 in e:\anaconda\envs\autog\lib\site-packages (from requests->autogluon.multimodal==0.6.2->autogluon.text) (2022.12.7)
> Requirement already satisfied: urllib3<1.27,>=1.21.1 in e:\anaconda\envs\autog\lib\site-packages (from requests->autogluon.multimodal==0.6.2->autogluon.text) (1.26.15)
> Requirement already satisfied: idna<4,>=2.5 in e:\anaconda\envs\autog\lib\site-packages (from requests->autogluon.multimodal==0.6.2->autogluon.text) (2.6)
> Requirement already satisfied: PyWavelets>=1.1.1 in e:\anaconda\envs\autog\lib\site-packages (from scikit-image<0.20.0,>=0.19.1->autogluon.multimodal==0.6.2->autogluon.text) (1.4.1)
> Requirement already satisfied: tifffile>=2019.7.26 in e:\anaconda\envs\autog\lib\site-packages (from scikit-image<0.20.0,>=0.19.1->autogluon.multimodal==0.6.2->autogluon.text) (2023.3.15)
> Requirement already satisfied: imageio>=2.4.1 in e:\anaconda\envs\autog\lib\site-packages (from scikit-image<0.20.0,>=0.19.1->autogluon.multimodal==0.6.2->autogluon.text) (2.26.0)
> Requirement already satisfied: threadpoolctl>=2.0.0 in e:\anaconda\envs\autog\lib\site-packages (from scikit-learn<1.2,>=1.0.0->autogluon.multimodal==0.6.2->autogluon.text) (3.1.0)
> Requirement already satisfied: filelock in e:\anaconda\envs\autog\lib\site-packages (from transformers<4.24.0,>=4.23.0->autogluon.multimodal==0.6.2->autogluon.text) (3.10.0)
> Requirement already satisfied: tokenizers!=0.11.3,<0.14,>=0.11.1 in e:\anaconda\envs\autog\lib\site-packages (from transformers<4.24.0,>=4.23.0->autogluon.multimodal==0.6.2->autogluon.text) (0.13.2)
> Requirement already satisfied: botocore<1.30.0,>=1.29.92 in e:\anaconda\envs\autog\lib\site-packages (from boto3->autogluon.multimodal==0.6.2->autogluon.text) (1.29.94)
> Requirement already satisfied: s3transfer<0.7.0,>=0.6.0 in e:\anaconda\envs\autog\lib\site-packages (from boto3->autogluon.multimodal==0.6.2->autogluon.text) (0.6.0)
> Requirement already satisfied: jmespath<2.0.0,>=0.7.1 in e:\anaconda\envs\autog\lib\site-packages (from boto3->autogluon.multimodal==0.6.2->autogluon.text) (1.0.1)
> Collecting partd>=0.3.10
> Downloading http://pypi.doubanio.com/packages/4d/ea/879a276326ed87ab2595c13bb1d43ba49a2e435386417e95bf23b131a209/partd-1.3.0-py3-none-any.whl (18 kB)
> Requirement already satisfied: toolz>=0.8.2 in e:\anaconda\envs\autog\lib\site-packages (from dask<=2021.11.2,>=2021.09.1->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (0.12.0)
> Requirement already satisfied: cloudpickle>=1.1.1 in e:\anaconda\envs\autog\lib\site-packages (from dask<=2021.11.2,>=2021.09.1->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (2.2.1)
> Requirement already satisfied: pyarrow>=6.0.0 in e:\anaconda\envs\autog\lib\site-packages (from datasets>=2.0.0->evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (11.0.0)
> Requirement already satisfied: aiohttp in e:\anaconda\envs\autog\lib\site-packages (from datasets>=2.0.0->evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (3.8.4)
> Collecting tblib>=1.6.0
> Downloading http://pypi.doubanio.com/packages/f8/cd/2fad4add11c8837e72f50a30e2bda30e67a10d70462f826b291443a55c7d/tblib-1.7.0-py2.py3-none-any.whl (12 kB)
> Collecting sortedcontainers!=2.0.0,!=2.0.1
> Downloading http://pypi.doubanio.com/packages/32/46/9cb0e58b2deb7f82b84065f37f3bffeb12413f947f9388e4cac22c4621ce/sortedcontainers-2.4.0-py2.py3-none-any.whl (29 kB)
> Requirement already satisfied: msgpack>=0.6.0 in e:\anaconda\envs\autog\lib\site-packages (from distributed<=2021.11.2,>=2021.09.1->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (1.0.5)
> Collecting tornado>=6.0.3
> Downloading http://pypi.doubanio.com/packages/1c/26/cbfa1103e74a02e09dd53291e419da3ad4c5b948f52aea5800e6671b56e0/tornado-6.2-cp37-abi3-win_amd64.whl (425 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 425.3/425.3 kB 3.3 MB/s eta 0:00:00
> Requirement already satisfied: jinja2 in e:\anaconda\envs\autog\lib\site-packages (from distributed<=2021.11.2,>=2021.09.1->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (3.1.2)
> Collecting zict>=0.1.3
> Downloading http://pypi.doubanio.com/packages/a2/9d/e6b14a2627ead7692fcccbed526de1c88d026fd9e6332ddbd67b6a976401/zict-2.2.0-py2.py3-none-any.whl (23 kB)
> Requirement already satisfied: six in e:\anaconda\envs\autog\lib\site-packages (from hyperopt<0.2.8,>=0.2.7->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (1.16.0)
> Requirement already satisfied: py4j in e:\anaconda\envs\autog\lib\site-packages (from hyperopt<0.2.8,>=0.2.7->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (0.10.9.7)
> Requirement already satisfied: future in e:\anaconda\envs\autog\lib\site-packages (from hyperopt<0.2.8,>=0.2.7->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (0.18.3)
> Requirement already satisfied: zipp>=3.1.0 in e:\anaconda\envs\autog\lib\site-packages (from importlib-resources>=1.4.0->jsonschema<=4.8.0->autogluon.multimodal==0.6.2->autogluon.text) (3.15.0)
> Requirement already satisfied: virtualenv in e:\anaconda\envs\autog\lib\site-packages (from ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (20.21.0)
> Requirement already satisfied: aiosignal in e:\anaconda\envs\autog\lib\site-packages (from ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (1.3.1)
> Collecting grpcio<=1.43.0,>=1.32.0
> Downloading http://pypi.doubanio.com/packages/f6/1c/8c0698fabdb627ad4eb3723761efffdd0cd67c0e61256c16d6a392ef273c/grpcio-1.43.0-cp38-cp38-win_amd64.whl (3.4 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.4/3.4 MB 1.3 MB/s eta 0:00:00
> Collecting click
> Downloading http://pypi.doubanio.com/packages/4a/a8/0b2ced25639fb20cc1c9784de90a8c25f9504a7f18cd8b5397bd61696d7d/click-8.0.4-py3-none-any.whl (97 kB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 97.5/97.5 kB 2.7 MB/s eta 0:00:00
> Requirement already satisfied: protobuf<4.0.0,>=3.15.3 in e:\anaconda\envs\autog\lib\site-packages (from ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (3.20.3)
> Requirement already satisfied: frozenlist in e:\anaconda\envs\autog\lib\site-packages (from ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (1.3.3)
> Requirement already satisfied: tensorboardX>=1.9 in e:\anaconda\envs\autog\lib\site-packages (from ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (2.6)
> Requirement already satisfied: markdown>=2.6.8 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (3.4.1)
> Requirement already satisfied: tensorboard-data-server<0.8.0,>=0.7.0 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (0.7.0)
> Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (0.4.6)
> Requirement already satisfied: wheel>=0.26 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (0.38.4)
> Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (1.8.1)
> Requirement already satisfied: google-auth<3,>=1.6.3 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (2.16.2)
> Requirement already satisfied: werkzeug>=1.0.1 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (2.2.3)
> Collecting tensorboard>=2.9.1
> Downloading http://pypi.doubanio.com/packages/6f/77/e624b4916531721e674aa105151ffa5223fb224d3ca4bd5c10574664f944/tensorboard-2.11.2-py3-none-any.whl (6.0 MB)
>   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.0/6.0 MB 4.5 MB/s eta 0:00:00
> Requirement already satisfied: absl-py>=0.4 in e:\anaconda\envs\autog\lib\site-packages (from tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (1.4.0)
> Collecting tensorboard-data-server<0.7.0,>=0.6.0
> Downloading http://pypi.doubanio.com/packages/74/69/5747a957f95e2e1d252ca41476ae40ce79d70d38151d2e494feb7722860c/tensorboard_data_server-0.6.1-py3-none-any.whl (2.4 kB)
> Requirement already satisfied: cycler>=0.10 in e:\anaconda\envs\autog\lib\site-packages (from matplotlib->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (0.11.0)
> Requirement already satisfied: contourpy>=1.0.1 in e:\anaconda\envs\autog\lib\site-packages (from matplotlib->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (1.0.7)
> Requirement already satisfied: fonttools>=4.22.0 in e:\anaconda\envs\autog\lib\site-packages (from matplotlib->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (4.39.0)
> Requirement already satisfied: kiwisolver>=1.0.1 in e:\anaconda\envs\autog\lib\site-packages (from matplotlib->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (1.4.4)
> Requirement already satisfied: pyparsing>=2.3.1 in e:\anaconda\envs\autog\lib\site-packages (from matplotlib->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (3.0.9)
> Requirement already satisfied: ordered-set in e:\anaconda\envs\autog\lib\site-packages (from model-index->openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (4.1.0)
> Requirement already satisfied: markdown-it-py<3.0.0,>=2.2.0 in e:\anaconda\envs\autog\lib\site-packages (from rich->openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (2.2.0)
> Requirement already satisfied: pygments<3.0.0,>=2.13.0 in e:\anaconda\envs\autog\lib\site-packages (from rich->openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (2.14.0)
> Requirement already satisfied: yarl<2.0,>=1.0 in e:\anaconda\envs\autog\lib\site-packages (from aiohttp->datasets>=2.0.0->evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (1.8.2)
> Requirement already satisfied: async-timeout<5.0,>=4.0.0a3 in e:\anaconda\envs\autog\lib\site-packages (from aiohttp->datasets>=2.0.0->evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (4.0.2)
> Requirement already satisfied: multidict<7.0,>=4.5 in e:\anaconda\envs\autog\lib\site-packages (from aiohttp->datasets>=2.0.0->evaluate<=0.3.0->autogluon.multimodal==0.6.2->autogluon.text) (6.0.4)
> Requirement already satisfied: cachetools<6.0,>=2.0.0 in e:\anaconda\envs\autog\lib\site-packages (from google-auth<3,>=1.6.3->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (5.3.0)
> Requirement already satisfied: pyasn1-modules>=0.2.1 in e:\anaconda\envs\autog\lib\site-packages (from google-auth<3,>=1.6.3->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (0.2.8)
> Requirement already satisfied: rsa<5,>=3.1.4 in e:\anaconda\envs\autog\lib\site-packages (from google-auth<3,>=1.6.3->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (4.9)
> Requirement already satisfied: requests-oauthlib>=0.7.0 in e:\anaconda\envs\autog\lib\site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (1.3.1)
> Requirement already satisfied: importlib-metadata>=4.4 in e:\anaconda\envs\autog\lib\site-packages (from markdown>=2.6.8->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (6.0.0)
> Requirement already satisfied: mdurl~=0.1 in e:\anaconda\envs\autog\lib\site-packages (from markdown-it-py<3.0.0,>=2.2.0->rich->openmim<=0.2.1,>0.1.5->autogluon.multimodal==0.6.2->autogluon.text) (0.1.2)
> Collecting locket
> Downloading http://pypi.doubanio.com/packages/db/bc/83e112abc66cd466c6b83f99118035867cecd41802f8d044638aa78a106e/locket-1.0.0-py2.py3-none-any.whl (4.4 kB)
> Requirement already satisfied: MarkupSafe>=2.1.1 in e:\anaconda\envs\autog\lib\site-packages (from werkzeug>=1.0.1->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (2.1.2)
> Collecting heapdict
> Downloading http://pypi.doubanio.com/packages/b6/9d/cd4777dbcf3bef9d9627e0fe4bc43d2e294b1baeb01d0422399d5e9de319/HeapDict-1.0.1-py3-none-any.whl (3.9 kB)
> Requirement already satisfied: distlib<1,>=0.3.6 in e:\anaconda\envs\autog\lib\site-packages (from virtualenv->ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (0.3.6)
> Requirement already satisfied: platformdirs<4,>=2.4 in e:\anaconda\envs\autog\lib\site-packages (from virtualenv->ray[tune]<2.1,>=2.0->autogluon.core[raytune]==0.6.2->autogluon.multimodal==0.6.2->autogluon.text) (3.1.1)
> Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in e:\anaconda\envs\autog\lib\site-packages (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (0.4.8)
> Requirement already satisfied: oauthlib>=3.0.0 in e:\anaconda\envs\autog\lib\site-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=2.9.1->pytorch-lightning<1.8.0,>=1.7.4->autogluon.multimodal==0.6.2->autogluon.text) (3.2.2)
> Building wheels for collected packages: fairscale, antlr4-python3-runtime
> Building wheel for fairscale (pyproject.toml) ... done
> Created wheel for fairscale: filename=fairscale-0.4.6-py3-none-any.whl size=307237 sha256=322633f0853d8de2c58624778dd43c9f042b2358c65678f0b1c770d142906544
> Stored in directory: c:\users\pc\appdata\local\pip\cache\wheels\fc\ed\fb\45837505439e660493bee33ff1aa04228fb88aac006d579750
> Building wheel for antlr4-python3-runtime (setup.py) ... done
> Created wheel for antlr4-python3-runtime: filename=antlr4_python3_runtime-4.8-py3-none-any.whl size=141217 sha256=335f9f89b4ecb9aabdc046f2666334c6e507c8def0203e0c53596b8440f2dde1
> Stored in directory: c:\users\pc\appdata\local\pip\cache\wheels\97\00\56\ee5a640976aa25f5ed767e5f195e3de51c4a04b8bc3b67e96c
> Successfully built fairscale antlr4-python3-runtime
> Installing collected packages: typish, sortedcontainers, heapdict, antlr4-python3-runtime, zict, tornado, torch, tensorboard-data-server, tblib, smart-open, scipy, opencv-python-headless, omegaconf, nptyping, locket, grpcio, click, torchvision, torchtext, scikit-learn, partd, jsonschema, fairscale, accelerate, transformers, ray, qudida, pytorch-metric-learning, nlpaug, dask, tensorboard, openmim, distributed, albumentations, pytorch-lightning, autogluon.common, autogluon.features, autogluon.core, autogluon.multimodal, autogluon.text
>
> Attempting uninstall: antlr4-python3-runtime
>  Found existing installation: antlr4-python3-runtime 4.9.3
>  Uninstalling antlr4-python3-runtime-4.9.3:
>    Successfully uninstalled antlr4-python3-runtime-4.9.3
> Attempting uninstall: torch
>  Found existing installation: torch 1.13.1
>  Uninstalling torch-1.13.1:
>    Successfully uninstalled torch-1.13.1
> Attempting uninstall: tensorboard-data-server
>  Found existing installation: tensorboard-data-server 0.7.0
>  Uninstalling tensorboard-data-server-0.7.0:
>    Successfully uninstalled tensorboard-data-server-0.7.0
> Attempting uninstall: smart-open
>  Found existing installation: smart-open 6.3.0
>  Uninstalling smart-open-6.3.0:
>    Successfully uninstalled smart-open-6.3.0
> Attempting uninstall: scipy
>  Found existing installation: scipy 1.10.1
>  Uninstalling scipy-1.10.1:
>    Successfully uninstalled scipy-1.10.1
> Attempting uninstall: omegaconf
>  Found existing installation: omegaconf 2.2.3
>  Uninstalling omegaconf-2.2.3:
>    Successfully uninstalled omegaconf-2.2.3
> Attempting uninstall: nptyping
>  Found existing installation: nptyping 2.4.1
>  Uninstalling nptyping-2.4.1:
>    Successfully uninstalled nptyping-2.4.1
> Attempting uninstall: grpcio
>  Found existing installation: grpcio 1.51.3
>  Uninstalling grpcio-1.51.3:
>    Successfully uninstalled grpcio-1.51.3
> Attempting uninstall: click
>  Found existing installation: click 8.1.3
>  Uninstalling click-8.1.3:
>    Successfully uninstalled click-8.1.3
> Attempting uninstall: torchvision
>  Found existing installation: torchvision 0.14.1
>  Uninstalling torchvision-0.14.1:
>    Successfully uninstalled torchvision-0.14.1
> Attempting uninstall: scikit-learn
>  Found existing installation: scikit-learn 1.2.2
>  Uninstalling scikit-learn-1.2.2:
>    Successfully uninstalled scikit-learn-1.2.2
> Attempting uninstall: jsonschema
>  Found existing installation: jsonschema 4.17.3
>  Uninstalling jsonschema-4.17.3:
>    Successfully uninstalled jsonschema-4.17.3
> Attempting uninstall: fairscale
>  Found existing installation: fairscale 0.4.13
>  Uninstalling fairscale-0.4.13:
>    Successfully uninstalled fairscale-0.4.13
> Attempting uninstall: accelerate
>  Found existing installation: accelerate 0.16.0
>  Uninstalling accelerate-0.16.0:
>    Successfully uninstalled accelerate-0.16.0
> Attempting uninstall: transformers
>  Found existing installation: transformers 4.26.1
>  Uninstalling transformers-4.26.1:
>    Successfully uninstalled transformers-4.26.1
> Attempting uninstall: ray
>  Found existing installation: ray 2.2.0
>  Uninstalling ray-2.2.0:
>    Successfully uninstalled ray-2.2.0
> Attempting uninstall: pytorch-metric-learning
>  Found existing installation: pytorch-metric-learning 1.7.3
>  Uninstalling pytorch-metric-learning-1.7.3:
>    Successfully uninstalled pytorch-metric-learning-1.7.3
> Attempting uninstall: nlpaug
>  Found existing installation: nlpaug 1.1.11
>  Uninstalling nlpaug-1.1.11:
>    Successfully uninstalled nlpaug-1.1.11
> Attempting uninstall: tensorboard
>  Found existing installation: tensorboard 2.12.0
>  Uninstalling tensorboard-2.12.0:
>    Successfully uninstalled tensorboard-2.12.0
> Attempting uninstall: openmim
>  Found existing installation: openmim 0.3.6
>  Uninstalling openmim-0.3.6:
>    Successfully uninstalled openmim-0.3.6
> Attempting uninstall: pytorch-lightning
>  Found existing installation: pytorch-lightning 1.9.4
>  Uninstalling pytorch-lightning-1.9.4:
>    Successfully uninstalled pytorch-lightning-1.9.4
> Attempting uninstall: autogluon.common
>  Found existing installation: autogluon.common 0.7.0
>  Uninstalling autogluon.common-0.7.0:
>    Successfully uninstalled autogluon.common-0.7.0
> Attempting uninstall: autogluon.features
>  Found existing installation: autogluon.features 0.7.0
>  Uninstalling autogluon.features-0.7.0:
>    Successfully uninstalled autogluon.features-0.7.0
> Attempting uninstall: autogluon.core
>  Found existing installation: autogluon.core 0.7.0
>  Uninstalling autogluon.core-0.7.0:
>    Successfully uninstalled autogluon.core-0.7.0
> Attempting uninstall: autogluon.multimodal
>  Found existing installation: autogluon.multimodal 0.7.0
>  Uninstalling autogluon.multimodal-0.7.0:
>    Successfully uninstalled autogluon.multimodal-0.7.0
> `ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
> autogluon-timeseries 0.7.0 requires autogluon.common==0.7.0, but you have autogluon-common 0.6.2 which is incompatible.
> autogluon-timeseries 0.7.0 requires autogluon.core[raytune]==0.7.0, but you have autogluon-core 0.6.2 which is incompatible.
> autogluon-tabular 0.7.0 requires autogluon.core==0.7.0, but you have autogluon-core 0.6.2 which is incompatible.
> autogluon-tabular 0.7.0 requires autogluon.features==0.7.0, but you have autogluon-features 0.6.2 which is incompatible.
> autogluon 0.7.0 requires autogluon.core[all]==0.7.0, but you have autogluon-core 0.6.2 which is incompatible.
> autogluon 0.7.0 requires autogluon.features==0.7.0, but you have autogluon-features 0.6.2 which is incompatible.
> autogluon 0.7.0 requires autogluon.multimodal==0.7.0, but you have autogluon-multimodal 0.6.2 which is incompatible.`
> Successfully installed accelerate-0.13.2 albumentations-1.1.0 antlr4-python3-runtime-4.8 autogluon.common-0.6.2 autogluon.core-0.6.2 autogluon.features-0.6.2 autogluon.multimodal-0.6.2 `autogluon.text-0.6.2` click-8.0.4 dask-2021.11.2 distributed-2021.11.2 fairscale-0.4.6 grpcio-1.43.0 heapdict-1.0.1 jsonschema-4.8.0 locket-1.0.0 nlpaug-1.1.10 nptyping-1.4.4 omegaconf-2.1.2 opencv-python-headless-4.7.0.72 openmim-0.2.1 partd-1.3.0 pytorch-lightning-1.7.7 pytorch-metric-learning-1.3.2 qudida-0.0.4 ray-2.0.1 scikit-learn-1.1.3 scipy-1.9.3 smart-open-5.2.1 sortedcontainers-2.4.0 tblib-1.7.0 tensorboard-2.11.2 tensorboard-data-server-0.6.1 torch-1.12.1 torchtext-0.13.1 torchvision-0.13.1 tornado-6.2 transformers-4.23.1 typish-1.9.3 zict-2.2.0