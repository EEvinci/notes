# Github-Blog

[TOC]



## hexo是什么

什么是Hexo？ Hexo 是一个快速、简洁且高效的**博客框架**。 

Hexo 使用Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成**静态网页**

## 为什么选择hexo和github

- 1、全是**静态文件**，不需要书写自己的后台逻辑，访问速度快
- 2、免费方便，不用花一分钱就可以搭建一个自己的个人博客
- 3、可以集成很多的插件，只需要简单配置
- 4、**样式多样可选，hexo有很多主题可供用户选择**(如果想自己写主题, 那么就不用hexo的主题)
- 5、自定义域名，可以绑定自己的域名
- 6、**数据绝对安全，基于github的版本管理，历史版本可随意恢复**
- 7、**数据容易迁移**

## 预安装node.js+Git

### node.js

安装Hexo非常容易，并且只需要以下内容：

- Node.js（至少应为Node.js 8.10，建议为10.0或更高版本）
- git

![image-20230128234940771](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230128234940771.png)

![image-20230128235006765](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230128235006765.png)

### git

SSH相关配置, 要与github建立连接

根据github邮箱配置对git相关配置进行修改

![image-20230129000031330](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129000031330.png)

#### 查看git相关配置

```cmd
git config --list
```

![image-20230129000145156](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129000145156.png)

#### 更改user.name或user.email

```cmd
git config --global user.name "Evinci"
git config --global user.email "evinciy@qq.com"
```

#### 生成ssh密钥, 这里使用的是rsa密钥

```cmd
ssh-keygen -t rsa -C "自己的邮箱"
```

之前已经生成过了, 现在生成需要覆盖

id_rsa 是私钥

id_rsa.pub 是公钥 放在GitHub上

![image-20230129001121319](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129001121319.png)

将你用户目录下 `.ssh/id_rsa.pub`里的全部东西粘贴到key里面，名字随便取。

`id_rsa.pub`一般windows会在 `C:\Users\用户名\.ssh`目录下.

![image-20230129000516145](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129000516145.png)

#### 验证

输入 `ssh-T git@github.com`，如果出现以下信息即为配置成功，到这里你已经成功了一大半了。

![image-20230129001456281](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129001456281.png)

## 安装Hexo

安装hexo:

```cmd
npm -i hexo-cli -g
```

中途升级下npm

```cmd
npm install -g npm@9.4.0
```

根据提示进行升级, 这时候npm版本就是最新的了

![image-20230128234402986](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230128234402986.png)

### 1. 检查hexo安装情况

![image-20230128234436462](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230128234436462.png)

### 2. 使用hexo初始化博客网站

在一个空的文件夹内打开cmd，使用 `hexo init` 进行初始化，他会下载一大堆东西。

```cmd
hexo init
```

![image-20230128234539279](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230128234539279.png)

![image-20230129001537157](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129001537157.png)

```shell
目录结构：
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

说明：

- node_modules：是依赖包
- public：存放的是生成的页面
- scaffolds：命令生成文章等的模板
- source：用命令创建的各种文章
- themes：博客使用的主题
- _config.yml：整个博客的配置
- db.json：source解析所得到的
- package.json：项目所需模块项目的配置信息

用npm安装相关的组件

```cmd
npm install
```

可能是之前下载过, 现在是更新了

![image-20230129001746390](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129001746390.png)

### 3. 生成博客

只需要三句话你就能看到你的博客

```javascript
1、清除hexo clean

2、生成hexo generate(g)

3、启动服务hexo server(s)
```

输入`hexo g`生成静态网页，然后输入`hexo s`打开本地服务器，然后浏览器打开`http://localhost:4000/`，就可以看到我们的博客啦

![image-20230129002147815](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129002147815.png)

![image-20230129002259769](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129002259769.png)

![image-20230129002250819](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129002250819.png)

### 4、上传至github

当然，如果只能自己看到，这远远是不够的，我们发博客就是为了让我们的文章能够帮助到更多人，这时候你就需要上传到github进行托管，这样别人就可以访问到你的博客，看到你的文章了。

你需要修改在你的根目录下的_config.yml配置

![image-20230129003840624](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129003840624.png)

然后使用 `hexo d` 或者 `hexo deploy`上传，它实现的原理就是将您的Hexo文件夹的文件推送到存储库。

public/默认情况下，该文件夹不是（也不应该）上传的，请确保该.gitignore文件包含public/行。

文件夹结构应与此存储库大致相似，但不包含.gitmodules文件

#### Wrong-1

![image-20230129004212895](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129004212895.png)

此处的错误因为没有下载`hexo-deployer-git`插件, 在**站点目录**下输入下面的插件安装就好了：

```shell
npm install hexo-deployer-git --save
```

然后在使用`Hexo d`命令就可以推送了。

#### Wrong-2

在这里还可能出现spawn failed, 原因是网络问题, 可能开了代理, 重复多试几次就好



在vscode中使用powershell同时修改yml文件更加方便😊

![image-20230129004513323](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20230129004513323.png)

### 写文章、发布文章

要创建新帖子或新页面，可以运行以下命令：

```javascript
$ hexo new [layout] <title>

例如
$ hexo new hello
INFO  Created: D:\Projects\HEXO\text\source\_posts\hello.md
```

他就会在 `source/_posts`目录下生成一个md文件 `hello.md`

post是默认设置layout，但您可以提供自己的。

您可以通过在中编辑 `default_layout`设置来更改默认布局 `_config.yml`。

### 创建新的hexo页面

```shell
hexo new page <title>
```



## 参考文档

[hexo d命令报错 ERROR Deployer not found: git](https://blog.csdn.net/qq_21808961/article/details/84476504)

[Hexo错误：spawn failed的解决方法](https://blog.zhheo.com/p/128998ac.html)

[Github + Hexo 搭建个人博客](https://zz2summer.github.io/github-hexo-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)