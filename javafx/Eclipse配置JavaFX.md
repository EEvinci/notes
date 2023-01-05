# Eclipse配置JavaFX

[open javafx 文档](https://openjfx.io/openjfx-docs/)

### 下载`e(fx)clipse`

**因为eclipse中没有Java FX项目的创建选项, 所以需要下载插件`e(fx)clipse`来添加Java FX的可用选项**

1. 打开 **Eclipse**，点击菜单 **Help -> Install New Software**，如下图所示 -

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/809140126_34000.png)

2. 在上图的新弹出界面中选择 “Add”，如下图所示 -

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/597140127_14451.png)

   

   **在下载地址中输入:**

   ```java
   http://download.eclipse.org/efxclipse/updates-released/2.3.0/site
   ```

   

   然后点击“**OK**”，如下图所示-

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/516140129_78516.png)

   

   显示安装的所有详细信息 :

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/351140131_65599.png)

   

   同意协议，然后安装 :

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/808140131_12878.png)

   

   安装完成后，重新启动**Eclipse**:

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/324140133_97194.png)

3. 安装后的检查

   成功安装并重新启动**Eclipse**后，可以检查安装的结果。
   在**Eclipse**中选择：

   - **File -> New -> Others…**

   应该会看到有执行JavaFX编程的向导，如下图所示 :

   ![img](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/268140135_82027.png)

### 下载并导入Java FX的`jar包`

> JDK8、JDK9、JDK10默认带JAVAFX依赖包，从JDK11开始JAVAFX被默认移除，因此JDK11以上版本开发JAVAFX项目需要单独引入JAVAFX依赖包

自JDK 11开始，JavaFX 包被剥离出来了，创建 Java FX Applicattion 时需要手动添加依赖包，**并添加 VM options参数**

[JavaFX-jar下载](https://gluonhq.com/products/javafx/)

---**根据自己的操作系统选择32位还是64位, 类型Type一定是`SDK`:** 

![image-20220925225541611](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925225541611.png)



**---导入时可以为javaFX单独创建一个库:**

**点击`module path`, 添加库:**

![image-20220925225120986](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925225120986.png)



**---选择用户库:**

![image-20220925225226928](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925225226928.png)



**---点击用户库选项:**

![image-20220925225756471](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925225756471.png)



---**点击用户库, 然后新建库:**

![image-20220925225901408](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925225901408.png)



**---为新建的库命名:**

![image-20220925225915279](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925225915279.png)



**---选中新建的库:** 

​	添加外部jar: **从系统目录中选择添加,** 是jar文件的**绝对路径**

​	添加jar: 是已经将jar文件放在项目文件夹下之后, 可以**从项目中添加jar文件,** 是jar文件的**相对路径**

![image-20220925230047092](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925230047092.png)

**最后应用并关闭即可**

[参考文档](https://blog.csdn.net/weixin_49552238/article/details/120478178)



### 配置VM语句环境配置

#### **VM语句:**

**不要搬引号中的路径, 填入自己Java FX-jar包所在的lib文件夹的路径**

```java
--module-path "E:\JavaSoftware\JavaFX_jar\openjfx-19_windows-x64_bin-sdk\javafx-sdk-19\lib" --add-modules javafx.controls,javafx.fxml
```



#### 配置步骤:

**---在运行中点击`Coverage Configurations`:**

![image-20220925230444431](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925230444431.png)



---**关键步骤: 如果用的是红色字体标注的过程, 蓝色的字体就可以忽略了, 配置已经成功了**

**文本框VM自变量中填入以下语句:**

(**ps:不要搬引号中的路径, 填入自己Java FX-jar包所在的lib文件夹的路径**)

```java
--module-path "E:\JavaSoftware\JavaFX_jar\openjfx-19_windows-x64_bin-sdk\javafx-sdk-19\lib" --add-modules javafx.controls,javafx.fxml
```

![image-20220925230952690](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925230952690.png)

--------

**---如果是有点管理强迫症的, 希望管理方便, 在创建新的Java FX项目时不用再输入一遍的话就按照蓝色的字体描述进行配置**, 可以往下面继续看:

**点击变量, 在出来的新窗口中点击编辑变量:**

![image-20220925231221703](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925231221703.png)



**---点击新建:**

![image-20220925231326589](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925231326589.png)



---**名称可以填:`JavaFX.control`**

![image-20220925231622854](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925231622854.png)

**值中填入以下语句:**

(**ps:不要搬引号中的路径, 填入自己Java FX-jar包所在的lib文件夹的路径**)

```java
--module-path "E:\JavaSoftware\JavaFX_jar\openjfx-19_windows-x64_bin-sdk\javafx-sdk-19\lib" --add-modules javafx.controls,javafx.fxml
```



---**然后在选择变量的窗口选择自己刚刚创建的变量使用即可**:

![image-20220925231900409](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220925231900409.png)



**至此就全部配置成功了**

[参考文档](https://blog.csdn.net/CHINA_CNN/article/details/105988824)

