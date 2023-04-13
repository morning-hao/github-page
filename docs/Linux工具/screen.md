##


# 一、安装`screen`

```bash
sudo apt-get install screen
```

# 二、基本操作

- 列出所有会话：

  ```bash
  screen -ls
  ```

- 恢复会话：

  ```bash
  screen -r [会话ID]
  ```

- 新建命名会话：

  ```bash
  screen -S [会话名称]
  ```

  

# 三、快捷键

- 分离当前会话：`Ctrl-a d`
- 切换下一个窗口：`Ctrl-a n`
- 切换上一个窗口：`Ctrl-a p`
- 创建新窗口：`Ctrl-a c`
- 关闭当前窗口：`Ctrl-a k`

# 四、python后台文件浏览器demo

一个使用`screen`启动`python3 -m http.server --cgi 45678`并让其在后台运行的示例：

1. 首先，新建一个命名会话。这里我们给会话命名为`http_server`：

   ```bash
   screen -S http_server
   ```

2. 现在，你将进入新创建的`screen`会话。在该会话中，运行以下命令启动HTTP服务器：

   ```bash
   python3 -m http.server --cgi 45678
   ```

3. HTTP服务器已经在端口`45678`上启动。为了让服务器在后台运行，需要将当前会话分离。按下`Ctrl-a d`，你将被分离出当前会话，返回到原始终端。

此时，HTTP服务器已在后台运行。如果需要重新连接到该会话，请使用以下命令：

```bash
screen -r http_server
```

如果需要关闭HTTP服务器，请重新连接到会话，然后按下`Ctrl-c`，最后输入`exit`来终止会话。
