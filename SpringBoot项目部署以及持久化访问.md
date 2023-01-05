# SpringBoot项目部署以及持久化访问

[TOC]

## 通过maven命令`install`/`package`打包jar包

在idea中打开项目

然后双击运行maven命令即可

![image-20221214123652744](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123652744.png)

如若`install`或者`package`成功, 会生成一个`target`文件夹, `target`文件夹有一个项目的`jar`文件

![image-20221214123632810](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123632810.png)

## 通过`Xshell`/ `Xftp`登录服务器

通过`Xftp`将jar包传入到Linux服务器的`home`路径下

![image-20221214123609057](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123609057.png)

## 配置服务器运行环境

- 将本地的`jdk`和`maven`**压缩包**同样通过`Xftp`上传到服务器

- 可以在`根目录`下分别建立两个目录`jdk`和`maven`

![image-20221214123304937](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123304937.png)

- 然后通过在Linux服务器中将压缩包解压   [zip解压命令参考](https://blog.csdn.net/shenyunsese/article/details/17556089)

![image-20221214123347707](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123347707.png)

- 解压后在`/etc/profile`文件中配置环境变量

```cmd
export JAVA_HOME=/jdk/jdk1.8.0_351
export MAVEN_HOME=/maven/apache-maven-3.6.3

export PATH=$JAVA_HOME/bin:$PATH:$MAVEN_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

- 配置好之后通过`java -version`和`mvn -version`检查配置是否成功

![image-20221214123222119](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123222119.png)

[流程参考文档](https://zhuanlan.zhihu.com/p/58388786)

## 进入jar包所在目录运行jar包

在环境配置好之后就可以进入jar包所在目录, 通过命令运行jar包了

可以先使用`java -jar xxx.jar`测试能否成功运行

## 编写shell脚本运行文件

如果上述jar包可以正常运行, 可写一个`shell脚本`然后让它一直运行在服务器的后台

![image-20221214123730997](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221214123730997.png)

```shell
# !/bin/sh
nohup java -jar /home/ruoyi.jar &
```

## 使用nohup进行持久化访问

### 安装nohup

```shell
# 安装配置nohup
cd /home
# 安装nohup
yum install coreutils
# 在bash_profile文件中配置nohup
vi ~/.bash_profile
# 在  PATH=$PATH:$HOME/bin   后添加   :/usr/bin
# 退出文件
# 使得文件配置生效
source ~./bash_profile
```

### 使用nohup命令运行程序

使用`nohup`命令, 使得进程**在系统后台不挂断地运行命令**，退出终端不会影响程序的运行

同时在命令最后加上一个`&`符号, 将这个任务放到后台去执行

如果怕手残或者其他异常情况发生的话, 可以加一层保险, 结合`screen`命令

## screen创建多终端会话

> screen 命令允许用户在一个窗口内**使用多个终端会话**，可以断开连接，也可以重新连接已断开连接的会话。 每个会话都可以恢复连接，这样就算会话断开了，用户也不必担心数据丢失，这正好解决了我们的问题。

### 先使用screen命令创建一个窗口

```shell
screen -S item #创建item窗口
```

### 然后在`home`目录下创建脚本文件

```shell
# 创建并编写item.sh脚本文件
vim item.sh
# 进入文件之后将以下内容写进去
# #!是说明脚本解释器路径的特殊表示符, 所以#之后的内容不会被作为注释处理
#!/bin/sh 
nohup java -jar xxx.jar &
# 然后退出保存脚本文件
```

### 在该窗口中运行脚本文件

```shell
# 运行脚本文件
sh item.sh
```

### 退出窗口

```shell
# 返回主窗口
# 同时按
Ctrl + A + D
# 然后这个窗口就和运行项目无关了, 可以做其他的任何事情
```

这时候就不用管这个项目的运行情况, 可以做其他事了



## 结束进程

### 搜索进程查看项目运行情况

```shell
# 但是进程查看不管哪个窗口查看都是统一的, 查看的都是后台正在运行的进程
# 所以是可以在主窗口把item窗口中运行的进程kill掉的
ps -ef | grep xxx(jar包名字)
```

### **通过pid可以kill掉进程**

```shell
kill -9 pid号
```





## 参考文档

[Linux脚本开头#!符号的含义](https://www.cnblogs.com/easonjim/p/6850319.html)

[screen命令使用](https://handerfly.github.io/linux/2019/03/31/Screan%E5%91%BD%E4%BB%A4%E7%9A%84%E4%BD%BF%E7%94%A8/)

[Linux 终端命令的末尾加上一个 & 符号的作用](https://blog.csdn.net/willingtolove/article/details/113933488)

[如何让部署在服务器上的项目一直保持运行状态](https://blog.csdn.net/Desiy/article/details/108856333)

[在Linux上部署Spring Boot项目](https://zhuanlan.zhihu.com/p/58388786)

[Linux下的压缩（zip）解压(unzip)缩命令](https://blog.csdn.net/shenyunsese/article/details/17556089)

[Linux nohup 命令](https://www.runoob.com/linux/linux-comm-nohup.html)