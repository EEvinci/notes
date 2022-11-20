# VScode配置Java开发环境
## JDK配置
 - 首先需要安装一个`JDK`
 如果安装了有`idea`的话可以不用再另外安装了, 因为`idea`自带的有`JDK`
 如果没有安装`idea`那么需要自己去安装一个`JDK`
 ![在这里插入图片描述](E:\Typora\ty_Photo\d60812ff47874467a98cca455d78fa58.png)
 我这里是下载了两个`JDK`, 一个是`idea`自带的, 另一个是exe格式安装的`JDK`
 事实上用`idea`自带的`JDK`就行了, 在写的时候我已经又把exe格式安装的`JDK`卸载了
- 安装完成`JDK`之后, 需要配置一下环境变量
`JDK`的位置
![JDK的位置](E:\Typora\ty_Photo\9f748744bbf44f469584e5a7aa17f6b4.png)
先配置一个`JAVA_HOME`
![先配置一个JAVA_HOME](E:\Typora\ty_Photo\e3ef429966344d3bb69590f90b91e3ac.png)
然后在path里面配置两个, **一个是`JDK`的`bin`目录, 一个是`JRE`的`bin`目录**
![在这里插入图片描述](E:\Typora\ty_Photo\132112d011954cb5a98ec80b49bba403.png)
**先配置`JAVA_HOME`, 再配置`path`里的变量的好处就是**: 当之后因为某种原因更换`JDK`后, 就只需要改变`JAVA_HOME`里面的目录就好, `path`中的不用变
- 配置好之后在`cmd`或者`powershell`中验证一下
分别输入`java` `javac` `java -version`
![在这里插入图片描述](E:\Typora\ty_Photo\321fac289f6d488fa5ac3b078b0e1bed.png)
![在这里插入图片描述](E:\Typora\ty_Photo\be861a0335ce4e47af57a12786da831f.png)
前两个显示出用法就说明可以了
![在这里插入图片描述](E:\Typora\ty_Photo\614958f8cd754a63be3b66b54473c476.png)
最后一个显示出版本信息就说明配置成功了

## VScode配置
 - 首先在`VScode`中安装一个java插件
![在这里插入图片描述](E:\Typora\ty_Photo\adf1b52706144e639d1c7eb30dc4bdd5.png)
这一个插件里面包含六个扩展, 所以安装这一个插件就行了

 - **重点重点**: 如果是已经在VScode中打开了存在`java`代码的项目(文件夹)再安装插件, 这时候会发现程序不仅**无法运行**还**无法添加`JDK`:**  因为此时`VScode`并不把该项目看作是一个Java项目, 所以应该按照下图顺序
![在这里插入图片描述](E:\Typora\ty_Photo\4ddd9ef99e934d6d9bfdd632c0950f72.png)
	 - 先使用`Ctrl+Shift+p`显示命令栏, 输入`Java:Create Java Project`, 从而创建一个Java项目, 在创建的时候选择`No build tools`, **然后把要进行操作的项目复制到这个新创建的Java项目中**	![在这里插入图片描述](E:\Typora\ty_Photo\3aa7f37087db490186bd157bbfab117d.png)
之后就会让选择一个创建Java项目的位置, 选择一个自己觉得合适的位置创建	 ![在这里插入图片描述](E:\Typora\ty_Photo\ce8bc7b002a64e749ac48ed6c2e8201e.png)
	 - 创建Java项目完成之后在`Ctrl+Shift+p`显示的命令栏中输入`Java:Configure Java Runtime`
	 在输入这个命令之后, 可能出现这个页面打不开的现象, 如下图
 **但是这时候不要急:** 先打开一个`java`程序, 等待java扩展激活, 然后`vscode`会自动检索`JDK`, 前提是已经在环境变量里面配置过`JDK`的位置了.
 ![在这里插入图片描述](E:\Typora\ty_Photo\ccc345bf4611412fb86b97486526d453.png)
 先打开一个`java`程序
 ![在这里插入图片描述](E:\Typora\ty_Photo\af96b366f4f946e1a8739aee66386b68.png)
 这时候再看, 该页面已经检索到环境变量配置的`JDK`
 ![在这里插入图片描述](E:\Typora\ty_Photo\8bff7a12466d4a82a8ae1f4b872747f8.png)

	 -  最后使用`Ctrl+Shift+p`显示命令栏, 输入`Java:Configure Classpath`, 在下图如下位置添加`mysql-connector-java.jar`连接文件
![在这里插入图片描述](E:\Typora\ty_Photo\f446eeeb167449fcbdf554b4b9f66a46.png)
在`mysql`安装的时候应该就有安装这个连接文件
![在这里插入图片描述](E:\Typora\ty_Photo\940a8ae159b248d1afb82f691921864d.png)
![在这里插入图片描述](E:\Typora\ty_Photo\b7fbbfac68ba403b98658a09a6927270.png)

-----
**至此就可以顺利在vscode中写java并连接数据库了**
![在这里插入图片描述](E:\Typora\ty_Photo\e833d1cb04b544dba176eb0a91ad35fc.png)