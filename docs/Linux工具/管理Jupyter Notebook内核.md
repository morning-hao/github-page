##



# 管理Jupyter Notebook内核：添加、查看和删除

> 简要介绍如何使用Jupyter Notebook对内核进行添加、查看和删除操作，并提供一个深度学习环境的示例。
>
> emmm，前提是conda已经装了对应的环境，不然没用~

## 一. 确认是否已安装ipykernel

切换到要添加的虚拟环境，然后运行以下命令：

```bash
python -m ipykernel --version
```

## 二. 安装ipykernel（如未安装）

```bash
python -m pip install ipykernel
```

## 三. 为Jupyter Notebook添加内核

```bash
python -m ipykernel install --user --name=kernelname --display-name showname
```

其中，`kernelname`是创建的文件夹名，`showname`是在Jupyter Notebook中展示的内核名。通常，我们将这两者与环境名保持一致，方便识别。

## 四. 查看Jupyter Notebook内核

```bash
jupyter kernelspec list
```

## 五. 删除Jupyter内核

```bash
jupyter kernelspec remove kernelname
```

## 六.示例：创建深度学习环境内核

假设你已创建一个名为`deep_learning`的虚拟环境，现在希望将其添加到Jupyter Notebook中。你可以按照以下步骤操作：

1. 切换到`deep_learning`虚拟环境。

2. 确认是否已安装ipykernel，如未安装，请安装。

3. 为Jupyter Notebook添加内核：

   ```bash
   python -m ipykernel install --user --name=deep_learning --display-name "Deep Learning"
   ```
   
4. 查看Jupyter Notebook内核，确认新内核已添加。

5. 如需删除内核，运行`jupyter kernelspec remove deep_learning`。

现在，你已成功为Jupyter Notebook添加了一个名为"Deep Learning"的内核，可以在该内核中运行深度学习相关代码。
