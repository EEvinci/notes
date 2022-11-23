# 设置GitHub SSH密钥

1. 首先查看本地是否有.ssh文件, 看一下自己之前有没有设置过SSH密钥

   打开 `Git Bash `后 运行` cd ~/.ssh `查看是否有该文件
   如果本地有**ssh密钥**的话会有`id_rsa`、`id_rsa.pub`、`known_hosts`等文件。
   如果没有的话运行上步骤命令就会**找不到文件**的提示

2. 如果有, 但是已经忘记密码了, 可以删除ssh

   复制并运行`rm -rf ~/.ssh/*`把现有的`ssh key`都删掉，**这句命令行如果多打一个空格，可能就要重装系统了，建议复制运行**。

3. 创建SSH密钥: 运行`ssh-keygen -t rsa -C “你的邮箱”`，注意填写真实邮箱。

4. **按回车三次**

   ![image-20220827191600528](E:\Typora\ty_Photo\image-20220827191600528.png)

   公钥就在`id_rsa.pub`文件中

   ![image-20220827192024881](E:\Typora\ty_Photo\image-20220827192024881.png)

5. 运行 `cat ~/.ssh/id_rsa.pub` ，得到一串东西，完整的复制这串东西

   最后面的邮箱不要复制, 可以注意到邮箱前面有一个空格就是为了和公钥区别开

   ![image-20220827192957186](E:\Typora\ty_Photo\image-20220827192957186.png)

6. 打开`GitHub`->`点击头像`->`setting`->`SSH adn GPG keys`->`New SSh key`

   ![image-20220827193202709](E:\Typora\ty_Photo\image-20220827193202709.png)

7. 输入title、把刚才复制的那段公钥粘贴到`key`中保存

   ![image-20220827193322556](E:\Typora\ty_Photo\image-20220827193322556.png)

8. 在GitHub显示已经添加成功之后, 在`git bash`中运行`ssh -T git@github.com`，你可能会看到这样的提示。

   输入`yse`

   ![image-20220827192314849](E:\Typora\ty_Photo\image-20220827192314849.png)

9. 然后如果你看到` Permission denied (publickey)`. 就说明你失败了，请回到第 1 步重来

   如果你看到 `Hi XXX! You’ve successfully authenticated, but GitHub does not provide shell access.`那就说明你成功了



# GitHub 忘记SSH密钥

如果之前稀里糊涂的设置过SSH密钥, 但是之后忘了, 那么**只能删除后重新创建一个新的`SSH密钥`**, 因为Git为了保证安全并**没有重新修改密码的功能**

1. 首页：查看本地是否有.ssh文件

   打开 `Git Bash `后 运行` cd ~/.ssh `查看是否有该文件
   如果本地有**ssh密钥**的话会有`id_rsa`、`id_rsa.pub`、`known_hosts`等文件。
   如果没有的话运行上步骤命令就会**找不到文件**的提示

2. 如果有, 但是已经忘记密码了, 可以删除ssh

   复制并运行`rm -rf ~/.ssh/*`把现有的`ssh key`都删掉，**这句命令行如果多打一个空格，可能就要重装系统了，建议复制运行**。

3. 创建SSH密钥: 运行`ssh-keygen -t rsa -C “你的邮箱”`，注意填写真实邮箱。

4. 按回车三次

   ![image-20220827191600528](E:\Typora\ty_Photo\image-20220827191600528.png)

   公钥就在`id_rsa.pub`文件中

   ![image-20220827192024881](E:\Typora\ty_Photo\image-20220827192024881.png)

5. 运行 `cat ~/.ssh/id_rsa.pub` ，得到一串东西，完整的复制这串东西, 最后面的邮箱不要复制, 可以注意到邮箱前面有一个空格就是为了和公钥区别开

   ![image-20220827192957186](E:\Typora\ty_Photo\image-20220827192957186.png)

6. 打开`GitHub`->`点击头像`->`setting`->`SSH adn GPG keys`->`New SSh key`

   ![image-20220827193202709](E:\Typora\ty_Photo\image-20220827193202709.png)

7. 输入title、把刚才复制的那段公钥粘贴到key中保存

   ![image-20220827193322556](E:\Typora\ty_Photo\image-20220827193322556.png)

8. 在GitHub显示已经添加成功之后, 在`git bash`中运行`ssh -T git@github.com`，你可能会看到这样的提示。

   输入yse

   ![image-20220827192314849](E:\Typora\ty_Photo\image-20220827192314849.png)

9. 然后如果你看到` Permission denied (publickey)`. 就说明你失败了，请回到第 1 步重来

   如果你看到 `Hi XXX! You’ve successfully authenticated, but GitHub does not provide shell access.`那就说明你成功了
   
   ![image-20220827192314849](E:\Typora\ty_Photo\image-20220827192314849.png)