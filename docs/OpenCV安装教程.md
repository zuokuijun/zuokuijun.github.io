

>  Ubuntu版本：Linux version 4.15.0-54-generic (buildd@lgw01-amd64-014) (gcc version 7.4.0 (Ubuntu 7.4.0-1ubuntu1~18.04.1))，具体版本为：**Linuxmint-19.2-cinnamon-64bit**
>
>  Open CV版本为4.5.2：具体的下载地址为[https://opencv.org/releases/](https://opencv.org/releases/)
>
>  安装过程主要参考了这两篇博客：
>
>  [https://zhuanlan.zhihu.com/p/118222087](https://zhuanlan.zhihu.com/p/118222087) (仅做参考，不可用)
>
>  [https://www.linuxprobe.com/linux-install-opencv.html](https://www.linuxprobe.com/linux-install-opencv.html)

## 一. OpenCV的下载

1、首先从OPenCV官网直接下载原代码，格式为ZIP。

<p align="center">
<img src="./images/opencv.jpg"/>
</p>
2、对下载的代码进行解压

* sudo unzip  opencv4.5.2.zip （对文件进行解压）
* sudo mkdir build （新建一个文件）
* cd  build （进入新建文件目录）

## 二. 生成makefile文件

```html
sudo cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

<p align="center">
<img src="./images/cmake.jpg"/>
</p>

## 三. 编译

```html
sudo make
```

<p align="center">
<img src="./images/make.jpg"/>
</p>

在编译过程中，参考博文一中的安装方式会出现各种问题，最常见的就是文件缺失，缺少某个头文件等，后续会牵引出更多的问题，因此最终在经过多次尝试后摈弃了该方法，直接采用第二个博文中的安装方式进行安装，编译过程也一直没有出现其他问题，编译进度到100%即证明编译成功

## 四. 安装

```html
sudo make install
```

## 五. 配置环境变量

* **sudo vim/etc/ld.so.conf.d/opencv.conf**

这个时候你可能打开文件可能是空白的，没有关系，在文件末尾添加保存并退出

* **/usr/local/lib**

执行生效命令：

* **sudo ldconfig**

继续打开：

* **sudo vim /etc/bash.bashrc**

在文件末尾添加写入：

* **export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig**

保存退出。

执行更新命令：

* **source /etc/bash.bashrc**
* **sudo updatedb**

## 六. 测试

如果测试OpenCV是否安装成功呢，网上很多的教程都是利用IDE新建工程，或者自己手动写一个测试程序，虽然该方法也能够起到测试的作用，但是中间可能会出现其他问题，导致浪费不必要的时间，最佳的方式是采用**OpenCV自带的测试程序**

* cd opencv-4.2.0/samples/cpp/example_cmake

* sudo mkdir build

* cd build

* sudo make ..

* Sudo make
  运行生成的可执行文件，此时可以调用摄像头采集图像，一般来说执行程序后便可看到画面

## 七、Qt Creator 关联Open CV 库

* 在新建工程的pro文件中，添加

  ```c++
  CONFIG += link_pkgconfig
  PKGCONFIG += opencv
  ```

* 引入头文件与命名空间

  ```c++
  #include <opencv2/core/core.hpp>
  #include <opencv2/highgui/highgui.hpp>
  #include <opencv2/imgproc/imgproc.hpp>
  #include <opencv2/opencv.hpp>
  using namespace std;
  using namespace cv;
  ```

  

