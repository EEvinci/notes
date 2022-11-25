# 更改utools的安装路径

# utools简介

uTools = your tools（你的工具集）
uTools 是一个极简、插件化的现代桌面软件，通过自由选配丰富的插件，打造得心应手的工具集合。
通过快捷键（默认 alt + space ）就可以快速呼出这个搜索框。你可以往输入框内粘贴文本、图片、截图、文件、文件夹等等，能够处理此内容的插件也早已准备就绪，统一的设计风格和操作方式，助你高效的得到结果。
一旦你熟悉它后，能够为你节约大量时间，即用即走、不中断、无干扰，让你可以更加专注地改变世界。

# 下载utools

官网下载地址：[utoolos](http://www.u.tools/)选择自己相应的操作系统版本下载即可。
![在这里插入图片描述](https://img-blog.csdnimg.cn/94b05dd2ad41499e8e4df3bacebcfa77.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAY2FpLTQ=,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/e4ea4dbdd9544cea801513b5e9dd52f6.png)
下载 完成后点击这个.exe文件进行安装，目前默认是安装在C盘的，这个我们后续进行更改，先不要管，完成安装，然后退出utools软件，我们更改他的安装路径。

# 更改utools的安装路径

按住Win+R键打开运行窗口，输入%APPDATA%，回车。
![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAY2FpLTQ=,size_20,color_FFFFFF,t_70,g_se,x_16.png)

打开了一个目录，找到uTools目录的路径，例如：
![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAY2FpLTQ=,size_16,color_FFFFFF,t_70,g_se,x_16.png)
“C:\Users\lenovo\AppData\Roaming\uTools”
或者你也可以点击桌面utools快捷方式右击选择打开文件位置也可以看到。
![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAY2FpLTQ=,size_15,color_FFFFFF,t_70,g_se,x_16.png)

***重点：***右键截切整个uTools目录没错就是剪切，放到你想要存放的位置，例如：“D:\utools”
记住之前的路径，下面借助一个命令mklink，这里使用mklink的/d命令即可
以管理员方式运行cmd命令行（避免权限不够的情况影响结果），输入如下命名（记得修改为自己uTools目录移动的路径），然后回车
mklink /d “C:\Users\lenovo\AppData\Roaming\uTools” “E:\Tools\uTools”
这里是给移动后的文件创建一个符号链接，返回之前的AppData目录中出现一个类似快捷方式的uTools目录，实际上只是作为一个快捷方式，这样就能够做到不占用C盘空间，将数据存到其他地方了。
![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/76331351f3204241a0d2337c4cdff94a.png)
图标已变化。