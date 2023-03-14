# Linux-`screen`相关命令

## screen 的创建、恢复、删除命令

- 创建：

  ```
  screen -S name
  ```

- 查看有多少会话：

  ```
  screen -ls
  ```

- 恢复：

  ```
  screen -r name
  ```

- 先恢复没有则创建：

  ```
  screen -R name
  ```

- 删除：

  ```
  screen -S name -X quit
  ```

  > name为你查看到的screen ID，改成你自己的screen ID即可，然后一个个删除后，再次执行`screen -ls`查询命令，确定只有一个了就是正常的了。

- 指定作业离线：

  ```
  screen -d name
  ```

`screen -ls` 查看已建的screen ID（**保持只有一个`xdd`会话，多的话可能运行不正常**）
`screen -r xdd`  连接已经创建的screen窗口
**screen已经是后台，不需要-d，不需要`nohup`**