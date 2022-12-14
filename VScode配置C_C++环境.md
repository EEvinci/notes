# VScode配置C/C++环境

**1./** 下载`minGW`编译器, 并配置环境变量

**2./** 在VScode中下载C/C++插件

**3./** 下载好之后做该插件版本的回退, **退回到1.8.4版本**, 因为这个版本还可以自动生成一些配置文件, 比如`settings.json`文件和`launch.json`文件

![image-20220812004025201](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220812004025201.png)

如果没有.vscode文件夹, 如下所示

一定要是1.8.4版本的C/C++扩展, 不然不会自动生成C/C++的配置文件的

![image-20221101044331752](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221101044331752.png)

点一下就行了, 会自动生成

如果是1.8.4之后的版本，例如下图中的1.12.4，可以生成配置文件模板，但是里面的具体信息还要自己配置，很麻烦

![image-20221101045048852](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221101045048852.png)

如果是1.8.4，那么里面的信息就会自动识别然后配置，很便捷

像下面这些信息，1.8.4版本的都是自动配置好的，再往后的版本就都要自己手动输入配置了

![image-20221101045416531](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221101045416531.png)

**4./** 把这行本来的`false`改成`true`, 这样就会出现一个编译运行的界面了

不然在终端中会出现一大堆的编译提示，输入和结果的输出都很不清晰

![image-20220812004320085](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220812004320085.png)



**5./** 

一定要保证cpp或c文件的命名**没有中文**，不然会出现报错

![image-20221101045827712](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221101045827712.png)

但是这个编译运行的界面会有**闪退**的问题, 所以要在每一个C/C++程序`return 0`前加上一句`system("pause");`.

