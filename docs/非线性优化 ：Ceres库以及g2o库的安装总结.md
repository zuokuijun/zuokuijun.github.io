# 非线性优化 ：Ceres库以及g2o库的安装总结

* ## **Ceres库的安装**

  1、 首先需要安装相关的依赖

     *  sudo apt-get install liblapack-dev libsuitesparse-dev libcxsparse3.1.2 libgflags-dev 
     *  sudo apt-get install libgoogle-glog-dev libgtest-dev

   2、如果安装时找不到**cxsparse** 或者其他的lib，需要添加下面的源

  ```cassandra
     找到文件并打开：sudo vi /etc/apt/sources.list   
     将源deb http://cz.archive.ubuntu.com/ubuntu trusty main universe添加到sources.list文件上方
     更新源 sudo apt-get update
     重复第一步的安装步骤
  ```

    3、Ceres库是来自谷歌的非线性优化库之前SLAM14给出的安装文件版本较老，可能会出现安装失败的情况，因此.  这里从github上下载最新的源代码来对其进行编译、安装；下载地址:[https://github.com/ceres-solver/ceres-solver](https://github.com/ceres-solver/ceres-solver)

  * 对文件进行解压：unzip  ceres-solver-master.zip

  * 编译、安装

    ```cassandra
    mkdir build
    cd build
    cmake ..
    make 
    sudo make install
    ```

    

* ## **g2o库的安装**

  1、这里g2o库的安装与Ceres库的安装步骤大致类似，源文件路径为:[https://github.com/Rainerkuemmerle/g2o](https://github.com/Rainerkuemmerle/g2o)

  2、同样需要安装相关的依赖，SLAM14讲给出的安装文件较老，可能与现存的依赖版本不对应，因此这里下载了对心 版本的源文件对其进行编译。

  ```cassandra
    libsuitesparse-dev
    qtdeclarative5-dev
    qt5-qmake
    libqglviewer-dev-qt5
  ```

  3、编译、安装

    ```c++
    mkdir build
    cd build
    cmake ..
    make 
    sudo make install
    ```

* ## 判断是否安装成功

  进入目录/usr/local/include/，查找目录下是否存在ceres以及g2o两个目录，若存在则基本可判断安装成功。
  
    

