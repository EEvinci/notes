### pip使用、pip.ini文件配置、镜像源更换

[TOC]



#### 查看当前python环境中安装的所有包以及版本

分为pip查看和conda查看

pip：`pip freeze`

conda：`conda list`

#### pip详细命令使用

##### pip包更新升级

```python
pip install --upgrade pip
```

##### pip安装其他包

```python
pip install 安装的包名
```

因为我这里已经将`pip.ini`文件中的配置设置为了豆瓣源(下载很快), 所以不用再后面再加`-i 某某源地址`, 这种方式是**临时使用某镜像源**

![image-20221012083509642](E:\Typora\ty_Photo\image-20221012083509642.png)

```python
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host=pypi.douban.com
```

##### **临时使用某镜像源**

```pyton
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 安装包名
```

###### 国内安装源：

中国科学技术大学 :[https://pypi.mirrors.ustc.edu.cn/simple](https://links.jianshu.com/go?to=https%3A%2F%2Fpypi.mirrors.ustc.edu.cn%2Fsimple)

清华：[https://pypi.tuna.tsinghua.edu.cn/simple](https://links.jianshu.com/go?to=https%3A%2F%2Fpypi.tuna.tsinghua.edu.cn%2Fsimple)

豆瓣：[http://pypi.douban.com/simple/](https://links.jianshu.com/go?to=http%3A%2F%2Fpypi.douban.com%2Fsimple%2F)

华中理工大学 :[http://pypi.hustunique.com/simple](https://links.jianshu.com/go?to=http%3A%2F%2Fpypi.hustunique.com%2Fsimple)

山东理工大学 :[http://pypi.sdutlinux.org/simple](https://links.jianshu.com/go?to=http%3A%2F%2Fpypi.sdutlinux.org%2Fsimple)

阿里云 http://mirrors.aliyun.com/pypi/simple/

##### pip.ini文件的配置方法:

打开cmd, 进入到`%APPDATA%`中

![image-20221012084754911](E:\Typora\ty_Photo\image-20221012084754911.png)

实际是这个路径`C:\Users\PC\AppData\Roaming`

在该目录下创建一个`pip`文件夹:

​	`C:\Users\PC\AppData\Roaming\pip`

在`pip`文件夹下创建`pip.ini`文件

![image-20221012084620608](E:\Typora\ty_Photo\image-20221012084620608.png)

##### 修改pip.ini文件的规则

```python
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host=pypi.douban.com
```

可以进行分布的信任配置, 比如采用豆瓣源, 只在下载的时候信任, 但是在其他时候不信任, 就可以按照上述的写法进行 (很无效且2)

所以建议都配置在`[global]`中

如下:

```python
[global]
index-url = http://pypi.douban.com/simple
trusted-host=pypi.douban.com
```

如果想更换镜像源只用修改`index-url`和`trusted-host`后面的内容

分别变为其他的镜像源地址即可

`trusted-host`中的内容就是`index-url`中`域名部分`

##### pip查看是否已经安装

```python
# pip show --files 安装包名
Name:SomePackage    # 包名
Version:1.0         # 版本号
Location:/my/env/lib/pythonx.x/site-packages   # 安装位置
Files:              # 包含文件等等
../somepackage/__init__.py
[...]
```

##### pip检查哪些包需要更新

```python
pip list --outdated
```

###### 遇到问题:

![image-20221012085424511](E:\Typora\ty_Photo\image-20221012085424511.png)

现在最新的pip要求源必须是https的，不然会报错：

```cmd
WARNING: The repository located at pypi.douban.com is not a trusted or secure host and is being ignored. If this repository is available via HTTPS we recommend you use HTTPS instead, otherwise you may silence this warning and allow it anyway with '--trusted-host pypi.douban.com'.
```

但是每次要加这么长的尾巴很不geek，在`pip.ini`里面加上

`trusted-host=pypi.douban.com`

![image-20221012085544880](E:\Typora\ty_Photo\image-20221012085544880.png)

我之前的`trusted-host=pypi.douban.com`可能限制在了`install`中了, 也就是只有下载的时候是信任的

但是在更新的时候还是不信任: 把`[install]`注释掉或者是删除掉, 使信任的范围在全局即可

![image-20221012085346223](E:\Typora\ty_Photo\image-20221012085346223.png)

```python
[global]
index-url = http://pypi.douban.com/simple
trusted-host=pypi.douban.com
```

##### pip升级包

```python
pip install --upgrade 要升级的包名
```

##### pip卸载包

```python
pip uninstall --upgrade 要升级的包名
```

##### pip参数解释

```python
pip --help
```







linux服务器上的

```cmd
[global]
  
index-url=https://pypi.tuna.tsinghua.edu.cn/simple

extra-index-url=http://pypi.douban.com/simple
extra-index-url-mirror=http://mirrors.aliyun.com/pypi/simple/http://mirrors.aliyun.com/pypi/simple/
timeout = 6000

[install]

trusted-host=
        pypi.tuna.tsinghua.edu.cn
        pypi.douban.com
        mirrors.aliyun.com

disable-pip-version-check = true
```





### 服务器pip的conf文件找不到

只能在终端里面用命令配置其他源

```py
pip install tensorflow -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com
```

