# Vscode、VS编译器冲突混乱问题

## 问题描述：

针对电脑同时安装了VS和VScode，VScode打开之前c的程序，出现以下报错：`VScode 检测到#include 错误,请更新includepath。`
![检测到#include 错误,请更新includepath。已为此翻译单元 禁用波形曲线](https://img-blog.csdnimg.cn/20210411151700325.png)

## 解决办法：

问题出在VScode同时安装了VS，（安装顺序是否有影响尚不确定），VScode会自动改成调用VS的编译器， 如果不需要的话，手动改回来应该就可以。	

### 我们在VScode界面输入`Ctrl + Shift + p`调出命令面板。

![image-20230219211356006](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230219211356006.png)

###  跳转到下面这个界面

将编译器改为mingw的编译器

![image-20230219211623001](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230219211623001.png)

![image-20230219211507766](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230219211507766.png)

### 选完之后修改`IntelliSense 模式`

![image-20230219211710809](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230219211710809.png)

![在这里插入图片描述](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/20210411154711663.png)

将其修改为`gcc-X64`



这时报错就消失了。