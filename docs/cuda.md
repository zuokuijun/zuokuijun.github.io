#  Windows 下PyTorch GPU 显卡的配置步骤

>参考文献：
>
>[Windows 安装 CUDA/cuDNN - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/99880204?from_voters_page=true)

1、首先使用命令`nvidia-smi`查看显卡的驱动以及cuda版本

<p align="center">
    <img src="./images/cuda.png" />
</p>

2、下载并安装cuda，需要根据显卡以及驱动的型号安装对应的版本。

下载地址：[[CUDA Toolkit 11.6 Update 2 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64)]([CUDA Toolkit 11.6 Update 2 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64))

3、下载cuDNN，下载之前需要注册Nvidia账号。下载地址为: [cuDNN Download | NVIDIA Developer](https://developer.nvidia.com/rdp/cudnn-download)。下载完成之后将压缩包解压到任意目录下，然后设置相关的系统变量。比如这里cuDNN所在路径为：E:\software\CUDA\cudnn\cudnn-windows-x86_64-8.4.0.27_cuda11.6-archive\bin

4、在Pytorch官网[Start Locally | PyTorch](https://pytorch.org/get-started/locally/)可以选择对应的安装方式以及版本下载安装Pytorch GPU版本







 
