# win11无法运行脚本文件

> 在对```powershell```进行个性化配置`oh-my-posh`软件的时候，`oh-my-posh`需要运行配置脚本文件`PROFILE`，由于win11默认防止执行不信任的脚本文件，导致安装过程无法正常进行。

### 解决方法：

1. 以管理员模式运行`powershell`

2. 执行命令`set-ExecutionPolicy RemoteSigned`

3. 若出现错误

   ![image-20220625150839976](http://evinci.oss-cn-hangzhou.aliyuncs.com/evinci/image-20220625150839976.png)

4. 连续输入以下命令行:

   - `Set-ExecutionPolicy -Scope CurrentUser`

   - `RemoteSigned`

其实就是将长命令分布执行, 在第一步的执行过程中将范围确定到当前用户进行执行