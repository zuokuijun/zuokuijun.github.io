# OpenFOAM5 安装教程

> `OpenFOAM`作为一个开源的`CFD`求解器，拥有庞大的用户群体。该文档主要记录安装`OpenFOAM`的过程，避免后续安装过程中继续踩坑
>
> Linux 系统:`ubuntu18.04`   安装软件：`OpenFOAM-5.X` 、`paraview-5.X`

 1、这里采用源码编译的形式进行安装 。首先在GitHub下载[OpenFOAM-5.X ZIP压缩包](https://github.com/OpenFOAM/OpenFOAM-5.x)以及[ThirdParty-5.x ZIP压缩包](https://github.com/OpenFOAM/ThirdParty-5.x)

2、在`/home/zuokuijun/`目录下新建`OpenFOAM`文件夹，并将下载的ZIP 压缩包移动到新建的文件目录下。

<p align="center">
    <img src="./images/openfoam1.png">
</p>

3、检查gcc版本：`gcc --version ;`如果提示没有安装，则按照提示安装`gcc sudo  apt-get  install  gcc`

​	安装OpenFOAM依赖：`sudo apt-get install build-essential flex bison git-core cmake  zlib1g-dev libboost-system-		dev libboost-thread-dev libopenmpi-dev  openmpi-bin gnuplot libreadline-dev libncurses-dev libxt-dev`

​	安装paraview依赖：`sudo apt-get install qt4-dev-tools libqt4-dev libqt4-opengl-dev freeglut3-dev libqtwebkit-dev curl`

4、配置环境变量：	在终端输入`gedit $HOME/.bashrc`

​	打开`.bashrc`文件，并下来到文件末尾，如果文件末尾存在类似source ...openfoam等语句，删除它，并重新添加下面

​	的语句；如果没有，直接添加即可。`source $HOME/OpenFOAM/OpenFOAM-dev/etc/bashrc`修改完`.bashrc`文件，保存并关闭文件。

​	关闭并重新打开终端，如果没有任何错误提示，则表示环境配置成功。

5、编译安装

​	进入到`OpenFOAM-5.x`文件夹下，终端键入`cd $HOME/OpenFOAM/OpenFOAM-5.x`。进入文件夹后，再次键入：`./Allwmake`

​	如果编译成功（在编译过程中没有弹出任何的错误提示），此时直接输入命令`blockMesh`，如果弹出下面这样的输出，说明编译成功：

<p align="center">
    <img src="./images/openfoam2.png"/>
</p>

6、编译完`OpenFOAM-5.x`之后，开始下载并编译`paraview`等第三方软件。	

​	进入到`Thirdparty-5.x`文件夹内，

​	`cd $HOME/OpenFOAM/ThirdParty-5.x`

​	然后继续键入：

​	`./Allwmake`

​	编译成功之后，继续键入：

​	`./makeParaView`

​	此时开始下载`paraview`，进而自动完成编译；注意，有些网络不好的情况下，在此处会提示下载失败，可多次尝试，或改用校园网。

​	下载编译`paraview`时间也会很长，大概一个小时左右，耐心等待。

​	此时在终端输入paraview会打开相应的软件界面

<p align="center">
	<img src="./images/openfoam3.png"/>
</p>




















