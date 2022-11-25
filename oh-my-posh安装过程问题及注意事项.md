在通过官方的安装命令后在个人用户的环境变量中有oh-my-posh的环境变量

![image-20220625153304583](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220625153304583.png)

但即使已经装配了环境变量，在powershell中输入`oh-my-posh`依然会出现未识别问题

![image-20220625153521779](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220625153521779.png)

这个问题的解决方法是: 通过管理员模式进入

然后就会发现之前设置的东西就回来了

------

# oh-my-posh安装过程问题及注意事项

> ### 截至2022年6月25日晚上8点，我已经彻底征服了oh-my-posh这个软件，对字体和主题的更换流程轻车熟路,还可以自己定做自己喜欢的主题(因为有现有主题的json文件所以可以对这些json文件进行修改填充自己想要的样式或者语句, 在不伤害原有主题的情况下另外创建一个json文件即完成了一个自己的主题)

[TOC]

## 软件安装

- 在官网找到对应的命令行，在`Windows timinal`中输入，进行安装

  - 如果没有`Windows Teminal`可以去微软应用商店里面搜索`Teminal`进行安装

  ![image-20220625200314261](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220625200314261.png)

  非常漂亮的一个界面，点击`Get Started`进入官方帮助文档内

- 现在我们已经进入到了文档内部, 看到真的非常详细, 有很多方面的指导说明![image-20220625200438478](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220625200438478.png)

- 通过`winget`方式使用以下命令行对`oh-my-posh`进行安装下载:

  ```shell
  winget install JanDeDobbeleer.OhMyPosh -s winget
  ```

  这个下载内容包括两个东西

  - `oh-my-posh.exe`-Windows executable

    这个是基于`Windows`系统的`oh-my-posh`的可执行文件, 但是**点击运行没有用**, 必须要在`Powershell`中执行

  - `themes`-The latest Oh My Posh [themes](https://ohmyposh.dev/docs/themes)

    **最新的主题**, 可以通过这个链接去官网主题页面进行查看下载

- 官方文档还贴出了`oh-my-posh`的更新命令, 如果是刚刚下载的那么就不需要更新了

  - ```shell
    winget upgrade JanDeDobbeleer.OhMyPosh -s winget
    ```

至此安装过程就已经全部完成了, 接下来是主题的配置

## 主题设置

- 首先要检查**环境变量**中有没有`POSH_THEMES_PATH`，通过环境变量中`POSH_THEMES_PATH`对应的路径可以找到所有可用的主题

- 然后使用以下这行命令进行主题的初始化, 其中`jandedobbeleer`是主题的名字

   ```shell
   oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json"
   ```

- 主题的更换要依托于一个`PROFILE`脚本文件来进行
   基于`PROFILE`脚本文件涉及到**创建**and**打开**and**填充配置语句**and**执行脚本文件**四条命令

   - 如果没有`PROFILE`文件：

      ```shell
      New-Item -Path $PROFILE -Type File -Force
      ```

   - 打开`PROFILE`文件：

      ```shell
      notepad $PROFILE
      ```

   - 在`PROFILE`文件中添加以下内容：

      ```txt
      oh-my-posh init pwsh | Invoke-Expression
      ```

   - 执行`PROFILE`脚本文件：
   
      ```shell
      . $PROFILE
      ```
   
   如果对以上流程还有一种云里雾里的感觉可以参看官方文档的[Prompt教程](https://ohmyposh.dev/docs/installation/prompt)
   
   ![image-20220626133312244](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626133312244.png)
   
   --------

## 字体乱码问题

- 在更换完主题之后可能会发现出现**小方框**, 也就是乱码问题, 是因为字体不适配的原因

- **解决方法:** 

  - 第一种: 去官网手动下载安装(**强烈推荐**，因为第二种我试了没弄好😁)

    - 在官方文档下载页面的初始几行就给出了与主题相适配的**书呆子**(`Nerd`)字体推荐

      ![image-20220626133835080](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626133835080.png) 

      所以需要去到[字体官网 Nerd Fonts](https://www.nerdfonts.com/)进行下载

      相关的界面再点击上图的`Nerd Font`就会去到官方的另一个界面[Fonts](https://ohmyposh.dev/docs/installation/fonts), 如下, 里面有详细的字体安装流程

      ![image-20220626134844825](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626134844825.png)

    - 下载下来的是一个压缩包文件, 将压缩包解压, 里面是字体文件的安装包, `Ctrl + a`全选然后选择**为全体用户安装**即可

    - 打开powershell的配置页面，选择外观->字体, 就可以发现已经有了, 然后选择保存, 开始使用

      ![image-20220626145141007](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626145141007.png)

      ![image-20220626145201224](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626145201224.png)

  - 第二种: 采用官方文档下载安装教程, **以管理员方式运行Teminal**用命令行进行安装

    - 一定要以管理员方式运行

      ```shell
      oh-my-posh font install
      ```

      下载页面情况如下

      ![image-20220626135743042](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626135743042.png)

      ![image-20220626135759109](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626135759109.png)

      ![image-20220626135831862](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626135831862.png)

    - 下载完成之后要在`Teminal`中进行配置

      ![image-20220626145344178](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626145344178.png)

      官方文档的解释是这样的

      ![image-20220626145507027](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626145507027.png)

      至此`oh-my-posh`就已经全部安装好了, 可以开始愉快的`powershell`命令行操作了🙌

      之后我会再看一下**创建自己的主题**和**在powershell导入Linux终端**连接自己的云服务器或者是Windows下的Linux子系统, 到时候总结一下再写出来

      -----------------

## 更换主题

在以上的安装步骤都顺利完成的基础上, 更换主题非常简单

```cmd
get-Poshthemes   //首先可以查看自己想要更换的主题
notepad $PROFILE    //打开配置脚本文件,内容形式如下
```

![image-20220626150139310](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626150139310.png)

就以上面的内容为例, 找到当前使用的主题名

![image-20220626150251620](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220626150251620.png)

然后将已经选择好的主题的名字替换原有的主题名

最后执行脚本, 使得更改生效, 主题更换即完成

```shell
. $PROFILE   //执行脚本文件命令
```



因为conda的原因所以想使用powershell的原主题, 用来显示环境名字, 所以保存一下PROFILE文件中的内容, 以后方便cv

```txt
oh-my-posh init pwsh --config C:\Users\PC\AppData\Local\Programs\oh-my-posh\themes/M365Princess.omp.json | Invoke-Expression
```







Ctrl+shift+K----->generate code line

```java
class name
{
    public static void main(String [],args)
    {
        System.out.println("hello world");
    }
}
```

