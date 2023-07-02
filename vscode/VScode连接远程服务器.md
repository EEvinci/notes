# VScode连接远程服务器

[toc]

## 下载扩展

下载以下三个扩展

`Remote-SSH`

`Remote - SSH: Editing Configuration Files`

`Remote Explorer`

![image-20230626145915241](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626145915241.png)

## 通过扩展连接服务器

下载完成之后vscode界面的左下角会出现一个如下的小图标

![image-20230626150100613](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626150100613.png)

点击小图标之后界面的正上方会出现如下选项，选择`Connect to Host`

![image-20230626150249687](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626150249687.png)

出现如下输入框

![image-20230626150945025](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626150945025.png)

### 在输入框中输入username@ip进行连接

例如要连接的服务器**IP为1.1.1.1**(举例)

使用账户的**用户名为cc**

那么即**按照提示**输入`cc@1.1.1.1`

如果是**第一次输入**, vscode会提供**保存配置文件以便于下次连接直接选择**的**配置文件保存选项**

可以选择**第一个配置文件**进行保存

![image-20230626152413867](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626152413867.png)

选择之后就会在**界面的右下角**出现一个**Host added的提示**

![image-20230626152636864](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626152636864.png)

这只是将**刚刚输入的服务器连接信息**写入到**ssh的config文件**中, 具有较高灵活性, 即**信息可以灵活更改**

其目的只是为了下次方便你的连接, 不需要再进行username@ip的服务器连接信息的输入

### 通过已保存的配置信息进行连接

你可以选择`Open Config`进行连接信息的查看和修改

HostName是要连接的主机名称, 可依据自己的喜好进行更改

Host是目标服务器的IP，一定要填写正确

同时User也一定要是目标服务器存在的用户名

![image-20230626152926329](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626152926329.png)

然后**重新点击界面左下角的绿色图**标进入**连接选项**, 即可看到出现了**刚保存的HostName**, 可以**点击**直接进行连接

![image-20230626153121227](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626153121227.png)

然后vscode会**打开一个新的界面**, 即进入服务器的连接, 如下所示, 第一次连接要对目标服务器进行**操作系统类型的判断**, 这里连接的是Linux服务器, 就选择Linux

![image-20230626153526400](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626153526400.png)

选择之后, 如果能够访问目标服务器, 那么就会弹出**密码的输入框**, 如下所示

![image-20230626153734260](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626153734260.png)

如果弹出以下提示, 说明连接目标服务器出现了问题, 请检查:

- ip是否输入错误
- 用户名是否输入错误
- 对目标服务器是否具有访问权限
- ...

![image-20230626153900382](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626153900382.png)

这里肯定无法连接, 因为该服务器根本不存在, 就更别提用户名和访问权限了

## 连接成功之后访问服务器文件

在连接成功之后, 界面不会进行跳转或弹出提示框

只会在终端显示连接信息

![image-20230626154112783](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626154112783.png)

看到了`Got connection`即说明连接成功了

### 访问文件

选择左边的文件图标, 可以看到显示`已连接到远程`, 这也是是否连接成功的一个判断标志

![image-20230626164551627](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230626164551627.png)

然后选择**打开文件夹**, 在选择指定的目录之后, 还需要**再输入一次密码, 才能成功打开**

