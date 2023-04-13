## 

# 一，镜像网站

https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/

# 二，安装后最好先安装的工具

```bash
sudo apt-get install vim
sudo apt-get install net-tools
sudo apt-get install lshw
sudo apt update
sudo apt upgrade
```



# 三，nvidia-smi相关的坑

下面是nvidia-driver和cuda版本的对应表，一般安装新的nvidia-driver就行

https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html

## 1.安装方法

> 先安装nvidia driver然后再分别安装cuda跟cudnn，安装可以在软件更新器里面自动安装，如果出现了nvidia-smi用不了的错误，尝试下dkms重装一次，要是还是不行先更新包索引和升级包再重启，重启后网络如果没了参考第二点恢复

## 2.恢复有线网络

参考文章：https://zhuanlan.zhihu.com/p/416061504

```bash
sudo touch /etc/NetworkManager/conf.d/10-globally-managed-devices.conf
sudo systemctl restart NetworkManager
```

