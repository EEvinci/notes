# 通过官网下载
![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/a4eb3eae42bc44dca2e34e59f67ca45a.png)
点击`DOWNLOAD`之后进入一个新的页面
![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/3d420539208c41e289d637c2a6d1f973.png)
下拉该页面, 找到`Community Download`
![](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/959540943e774650bb1358a8cae2919a.png)
点击该选项, 进入以下新的页面

![image-20220819225708396](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819225708396.png)

选中`MYSQL Install for Windows`

![image-20220819231223937](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819231223937.png)

进入以下页面![image-20220819231244042](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819231244042.png)

选择第二个![image-20220819231258197](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819231258197.png)

也就是所谓的`离线版下载`

下载完成后进行安装



# 安装

![image-20220819231405589](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819231405589.png)

安装界面是这样的, 因为我已经安装成功了, 所以显示的是`Welcome Back`

安装的要点如下:

1. 在第一页的安装方式选择中选择`custom`, 也就是自定义安装, 之后自己选择自己需要的组件, 而不是`Typical`把所有的组件全都安装上去, 有的其实并不需要
2. 安装的组件有三个必备的:`Workbench`, `Shell `, `Server`. 之后根据自己要使用的语言安装第四个连接的组件, 比如使用java就安装`Connector J `
3. 在勾选组件之后一定要点击下面的`Advance`选项用来改变组件的默认安装位置, 不然就会默认直接安装到C盘, 我比较在意这个事情. **ps**: 这个`Advance`是一行超级小的蓝字, 在界面的右下角, 一定要仔细和注意
4. 之后就是一路的next就行了, 中间输入以下自己mysql的密码, 普通用户创建可以创也可以不创, 没什么影响, 因为后面使用也是使用root用户

# 安装成功

安装成功之后, `shell`的环境变量是已经自动添加进去的,  但是`Server`的还没有添加, 需要自己手动添加以下. 

添加之后就可以在自己的cmd或者是powershell中使用mysql



- 先找到`Mysql Server`

![image-20220819232438023](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819232438023.png)

- 进入该文件夹中, 找到`bin`目录

  ![image-20220819232549915](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819232549915.png)

- 将bin目录的位置复制一下(这时候可以进入到bin目录里面, 然后复制上方的位置)

  ![image-20220819232716789](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819232716789.png)

- 打开环境变量的页面

  ![image-20220819232907693](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819232907693.png)

- 在`path`里面新建, 然后把`bin`目录的位置粘贴进去

  ![image-20220819233041867](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819233041867.png)

- 最后点三个确定保存操作即可

# 终端验证mysql环境变量配置

- 打开终端, 输入命令

```mysql
mysql -u root -p
```

- 输入在安装步骤中设置的root账户密码, 显示以下提示则说明配置正确

  ![image-20220819233337243](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819233337243.png)



# Mysql和Navicat连接

- 打开navicat

- 在`连接`中找到`Mysql`得到以下界面

  ![image-20220819233601460](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819233601460.png)

  为自己的这个数据库起一个名字, 什么名字都可以, 然后输入在安装步骤中设置的密码, 即可连接到自己的数据库

  ![image-20220819233701313](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220819233701313.png)

- 图表显示绿色就说明已经安装成功了