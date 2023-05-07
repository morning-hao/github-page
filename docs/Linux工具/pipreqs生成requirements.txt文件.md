##



# pipreqs生成requirements.txt文件

**GitHub仓库**：https://github.com/bndr/pipreqs

## 一. 安装pipreqs

```bash
pip install pipreqs
```

## 二. 生成requirements.txt文件

在当前目录下，使用以下命令生成`requirements.txt`文件：

```bash
pipreqs . --encoding=utf8 --force
```

## 三.示例

假设你有一个项目目录，项目结构如下：

```bash
my_project/
│
├── main.py
└── utils.py
```

在`main.py`和`utils.py`中，你使用了`requests`和`pandas`这两个库。此时，你可以打开终端，进入`my_project`目录，并运行上述命令(**pipreqs . --encoding=utf8 --force**)。生成的`requirements.txt`文件内容可能如下：

```bash
requests==2.26.0
pandas==1.3.3
```

**注意**：

- `--encoding=utf8`表示使用utf8编码，避免出现`UnicodeDecodeError: 'gbk'这样的`错误。
- `--force`表示强制执行，如果当前目录下已存在`requirements.txt`文件，将覆盖原文件。
