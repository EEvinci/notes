# tensorflow2.2.0安装过程

### 首先下载Anaconda

下载完成之后在终端中先为tensorflow建立一个环境
	

```python
conda create --name tensorflow_2.2.0 python=3.8
```
使用python3.8
网上很多人使用python3.5，3.5的pip最高只能到20，而最新的pip版本是22，因为在20年pip已经不对3.5进行最新版本的支持了，所以还是用python3.8好一些
之后的安装过程也会更加的顺利

##### 补充一下：用python3.8只能安装2.1.0以上的tensorflow

输入这个命令可以进入tensorflow环境
```python
conda activate tensorflow_2.2.0	
```
输入这个命令可以退出tensorflow环境
```python
conda deactivate
```

###   现在开始真正的tensorflow的安装
##### 刚刚只是给tensorflow在Anaconda中建立一个环境（给tensorflow建了一个房子，现在tensorflow可以住进去了）
输入这个命令，进行真正的tensorflow的安装
```python
pip install -i https://pypi.doubanio.com/simple tensorflow==2.2.0
```
然后就很顺利的完成了

完成之后可以在tensorflow环境中用pip查看一下安装的tensorflow的版本信息
```python
pip show tensorflow
```

至此就完美结束了

-----
发现anaconda中的环境可以嵌套使用，即在一个环境中激活另一个环境，当该环境退出时会回到第一个激活的环境，然后再退出才会回到base环境中
我现在有三个环境
![在这里插入图片描述](E:\Typora\ty_Photo\818cf90d011a4bb7b15e67bef81b72df.png)
现在我先进入TF2.1环境，再在TF2.1中进入Visual环境中
然后再依次从Visual和TF2.1中退出
因为这三个环境的python版本不同，所以可以用来作为区分
base环境python版本：3.7.4
TF2.1环境python版本：3.7.13
Visual环境python版本：3.8.13
![在这里插入图片描述](E:\Typora\ty_Photo\7f6b709d674a496880f1e0997111bd66.png)

------
在为环境安装包时，不要进入python中，激活环境然后通过pip命令进行下载

------
现在在power shell中通过设置使得能激活anaconda的虚拟环境了
但是害怕以后要通过powershell下载什么东西或者进行什么配置会直接下载或配置到base环境中
现在要把这个东西给取消掉
系统的终端设置还是要和anaconda的命令行管理分割一下
可以通过命令进入anaconda的管理模式
但是不能打开就默认进入