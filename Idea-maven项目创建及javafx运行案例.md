## maven项目创建及javafx运行案例

[TOC]

## maven项目创建

创建一个普通项目，**构建系统**使用**Maven**

![image-20221010194558504](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010194558504.png)



项目结构应该是这样的

![image-20221010194701916](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010194701916.png)

src下面有main和test

main下面有java和resources

test下面有java和test resources

test resources没有自动创建，为了完善项目结构一会手动创建一个



最关键的pom.xml文件初始化是这样的

![image-20221010195017017](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010195017017.png)

之后要根据项目的需要进行pom.xml文件的配置

**学习maven就是学习怎么配置pom.xml文件**



## maven + javafx项目配置

想创建一个javafx项目

#### 首先先把可能要添加的依赖理清楚

首先在pom.xml中添加关于javafx的依赖项

因为javafx中可能用到javafx.fxml, 所以也要添加javafx.fxml的依赖

可能之后要连接数据库, 所以要添加mysql-connector-java的依赖

#### 配置pom.xml文件

在添加之前, 要对pom文件的结构进行了解

可以格式化文档之后查看主次结构

以我这次配置的pom.xml文件为例

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!-- project是最高级 -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- 项目坐标 -->
    <groupId>groupId</groupId>
    <artifactId>fx1</artifactId>
    <version>1.0-SNAPSHOT</version>
    
    <!-- 依赖项添加 -->
    <dependencies>
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-controls</artifactId>
            <version>17.0.1</version>
        </dependency>

        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-fxml</artifactId>
            <version>17.0.1</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.28</version>
        </dependency>
    </dependencies>

    <!-- 构建项 -->
    <build>
        <!-- 添加插件 -->
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <!--                    <release>8</release>-->
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.3</version>
                <configuration>
                    <mainClass>sample.Main</mainClass>
                </configuration>
            </plugin>
        </plugins>

        <!--这我不知道是啥 之后查查-->
<!--        <resources>-->
<!--            <resource>-->
<!--                &lt;!&ndash; 这里是放在 src/main/java&ndash;&gt;-->
<!--                <directory>src/main/java</directory>-->
<!--                <includes>-->
<!--                    <include>**/*.properties</include>-->
<!--                    <include>**/*.fxml</include>-->
<!--                    <include>**/fxml/*.fxml</include>-->
<!--                    &lt;!&ndash; 如果想要弄个包名专门放fxml文件，像上一行这样添加设置 &ndash;&gt;-->
<!--                    &lt;!&ndash; 之后，使用getResource("fxml/xx.fxml")这样子 &ndash;&gt;-->
<!--                </includes>-->
<!--                <filtering>false</filtering>-->
<!--            </resource>-->
<!--        </resources>-->

    </build>

</project>
```

依赖dependency是添加在dependencies中的

<>代表开始

</>代表结束

![image-20221010204516764](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010204516764.png)

在pom.xml文件中使用alt+insert快捷键添加依赖项模板

将上面觉得可能要用到的依赖项添加进去

添加的时候有一个麻烦的点，要根据自己使用的软件的版本来说明依赖包的版本

比如上述依赖管理中，来自org.openjfx公司的javafx-controls依赖包和javafx-fxml依赖包就需要明确知道自己使用的jdk的版本，从而写明这两个依赖包的版本

来自mysql公司的mysql-connector-java依赖包就需要明确知道自己的mysql的版本，从而写明这个连接依赖包的版本

**所以要去cmd中查看自己一些软件的版本**

但是在idea中有小技巧，先填写依赖包的名称，然后在填写另外两个时候先按空格，idea就会自动显示一些版本，有可能准确有可能不准确（比如我的mysql版本是8，但是idea给我显示的链接依赖包的版本就只有5的），如果不准确要自己查询，然后输进去

> 一旦涉及到版本，就有可能出现软件之间的软件版本不对应的问题，比如mysql8就不能用5版本的连接依赖包

> ​	另外不止要添加依赖, 还要添加一些相应的插件
>
> 怎么知道要添加的插件名称我现在还不清楚

添加之后, 点击侧边栏的maven, 刷新配置文件

等待依赖项和插件下载完成, 程序就可以运行了

![image-20221010213623248](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010213623248.png)

相比之前要添加好几个jar包的方式方便很多

在用到很多不同的jar包时, 更能显示出maven这个依赖管理工具的便利性

-----

在运行javafx程序的时候, 要创建两个类, 一个app类, 一个appLaunch类, 因为运行Javafx程序要对**运行组件**进行检查

在maven构建下直接运行app类,会报错

![image-20221010214338038](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010214338038.png)

此时要创建一个运行app类的appLaunch类, 然后运行appLaunch, 才能正常运行

![image-20221010214442693](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221010214442693.png)

这个appLaunch类中只要一句话就行

```java
Application.launch(Login.class);
// 注意运行的是已经编译过的class文件
```

-------

#### 但是与此同时还是有一些问题没有解决，很难受：

1. 对pom.xml文件的详细配置还是不太清楚，可能每一次配置都要经过一大堆的搜索和试错，要继续看一些关于pom文件的文档
2. 对pom.xml文件中怎么搜寻相关需要的插件不清楚，就像这次案例，依赖项可以知道，但是有些插件不知道怎么获取，另外关于为什么要用到这些插件才能运行也不清楚
3. 为什么在maven构建下不能直接运行javafx的程序，必须要另外创建一个运行类；就像vscode中直接运行c/c++程序会出现运行窗口闪退，必须要加上一句system("pause");
4. 今天累了，先摸索到这，剩下的时间看一看数据结构，明天准备做助教

以上的问题纯粹是因为我新建的是普通项目，而不是Java FX项目，如果新建的是Java FX项目，那么idea会自动给你生成相应的需要的pom.xml文件，并且运行也是正常的

![image-20221017164152051](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20221017164152051.png)

------

#### 下一阶段搞明白javafx+maven+sceneBuilder

然后正式开始做javafx的界面

其实写代码才是最重要的

但是框架没有弄好我写不下去 差生文具多

写代码的时候要温习前两节课学的东西：泛型，lambda表达式

