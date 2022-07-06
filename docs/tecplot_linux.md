# Tecplot  Linux 版本安装

>引用知乎：[想学跳舞的码农](https://zhuanlan.zhihu.com/p/79897732)

今次工作需要在ubuntu 19.04上安装tecplot2015R1，花掉一个晚上的时间，具体什么原因也说不清，总之是装成了。给同样遇到困惑的小朋友分享一下。

### 1、下载破解版的文档（下载链接见底部）

### ![img](https://pic4.zhimg.com/80/v2-66eb4a6c6da1d97420097ebb1a88f3d3_720w.jpg)

### 2、安装

```bash
sudo bash tecplot360ex_2015_R1_linux64.sh
```

默认路径为

```bash
/usr/local/tecplot360ex
```

### 3、破解

将/usr/local/tecplot360ex 中的文件用*SolidSQUAD*中的相应文件替换

```bash
sudo cp dir/tecplot/_SolidSQUAD_/tecplotlm.lic /usr/local/tecplot360ex
sudo cp dir/tecplot/_SolidSQUAD_/bin/tec360-bin /usr/local/tecplot360ex/bin
```

### 4、配置环境文件

```bash
vim ~/.bashrc

export PATH="/usr/local/tecplot360ex/bin:$PATH"
export TECPHYFILE=$HOME/.tecplot.phy
export LD_LIBRARY_PATH="/usr/local/tecplot360ex/bin:$LD_LIBRARY_PATH"
export LD_LIBRARY_PATH="/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH"

source ~/.bashrc
```

讲道理，到这步应该就没问题了。但当我运行的时候却会出现如下错误提示：

![img](https://pic3.zhimg.com/80/v2-524bccbe766e9be2dea3ee0ab2a5949a_720w.jpg)

google了一下

```text
sudo mv /usr/local/tecplot360ex/bin/libfreetype.so.6 a.so.6
sudo mv /usr/local/tecplot360ex/bin/libz.so.1 a.so.6 b.so.1
```

这样就可以了。

![img](https://pic4.zhimg.com/80/v2-64916670f3536d7cac493e936d8cbb87_720w.jpg)

---



## 注意避坑！！！ 

自己在安装的时候发现，虽然软件能够正常打开，但是会导致其他软件用不了的情况，此时需要删除一下文件：

```bash
sudo mv /usr/local/tecplot360ex/bin/libz.so.1  /usr/local/tecplot360ex/bin/b.so.1
```

```
链接: https://pan.baidu.com/s/1Ntj_fuyLsErLZOksAjfLAA?pwd=cjku 提取码: cjku 复制这段内容后打开百度网盘手机App，操作更方便哦
```



