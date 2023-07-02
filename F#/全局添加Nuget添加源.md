# 全局添加Nuget添加源

## 安装nuget

官网下载地址：https://www.nuget.org/downloads

下载推荐的最新版本的即可

![image-20230530145131556](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230530145131556.png)

下载下来的只是一个exe文件，**不要直接点**，而是创建一个文件夹，然后将其放进去。

**使用命令行进行驱动**，即powershell或cmd

最好是**将其路径添加到环境变量中**，这样可以在任何位置使用nuget进行源的设置或相关操作

## 添加全局源

可以添加一个**官方源**和一个**镜像源**

```cmd
nuget sources add -Name "MyGet" -Source "https://dotnet.myget.org/F/dotnet-core/api/v3/index.json"

nuget sources add -Name "huaweicloud" -Source "https://mirrors.huaweicloud.com/repository/nuget/v3/index.json"
```

使用`nuget source`查看添加源的信息

![image-20230530145246351](https://evinci.oss-cn-hangzhou.aliyuncs.com/img/image-20230530145246351.png)