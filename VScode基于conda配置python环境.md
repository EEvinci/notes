# VScode基于conda配置python环境

**1./** 首先在VScode中下载python插件



**2./** 然后按住`ctrl+shift+p`，搜索`open setting`，会出现以下界面

![image-20220812003014885](E:\Typora\ty_Photo\image-20220812003014885.png)

选中绿框圈中的选项，创建一个`settings.json`文件，在里面输入`"python.condaPath": "E:\\Anaconda\\Scripts\\conda.exe"  `

![image-20220812003158250](E:\Typora\ty_Photo\image-20220812003158250.png)



**3./** 然后搜索`interpreter`, 会出现以下界面

![image-20220812003243908](E:\Typora\ty_Photo\image-20220812003243908.png)

点击这个有蓝色底框的选项添加解释器



**4./** 最后查看一下VScode最下面的解释器显示, 看是不是conda创建的虚拟环境的python解释器就可以了

