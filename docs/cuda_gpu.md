# Linux系统下驱动、cuda、的安装配置



## 一、驱动安装

去Nvidia官网下载GPU对应的驱动，进行相应的安装即可

[https://www.nvidia.com.tw/Download/index.aspx?lang=tw](https://www.nvidia.com.tw/Download/index.aspx?lang=tw)



## 二、cuda 安装

同样在Nvidia官网找到对应[cuda的下载地址](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=18.04&target_type=deb_local)进行下载安装。一般对于Linux 系统而言，其会直接给出对应的终端下载命令：比如我这里Ubuntu 18.04 版本下的安装命令为：

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.6.2/local_installers/cuda-repo-ubuntu1804-11-6-local_11.6.2-510.47.03-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-11-6-local_11.6.2-510.47.03-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu1804-11-6-local/7fa2af80.pub
sudo apt-get updatesudo apt-get -y install cuda
```

 

## 三、Cudnn安装

亲自尝试，发现及时不安装也是同样可以的，不影响使用，该软件下载需要注册nvidia账号
