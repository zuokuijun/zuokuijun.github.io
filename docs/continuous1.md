# 连续性方程（一）——流体微元

### 一、空间位置固定的无穷小流体微团连续方程的推导

<p align="center">
    <img src="./images/weituan1.png">
</p>


 欧拉观点下的质量守恒可以理解为：

位置固定的无穷小微团质量的变化 =  流入无穷小微团质量 - 流出无穷小微团质量

位置固定的无穷小微团质量的变化率=（流入无穷小微团质量 - 流出无穷小微团质量）的变化率

 流体微团的体积变化表示为$dV=dxdydz$，则此时无穷小流体微团的质量为：
$$
dm=\rho dxdydz
$$
  **根据质量变化率的定义（质量的变化除以时间的变化），可以表示为**：
$$
\frac{\partial dm}{\partial t}=\frac{\partial \rho dxdydz}{\partial t}=\frac{\partial \rho}{\partial t}dxdydz
$$
下面考虑无穷小流体微团的流入和流出。根据泰勒公式的定义：对于一个函数，$x_0$点的值为$f(x_0)$，那么$x_0+h$的值可以通过下述方程求得：
$$
f(x_0+h) \approx f(x_0)+f^`(x_0)h
$$
如图所示，针对无穷小流体微团而言，立方体左侧单位面积的质量流量为$\rho u$，其表示单位时间内流入单位面积的质量。同时立方体左侧的面积为$dydz$，因此有单位时间内流入的质量为$\rho u dy dz$。而对于立方体右侧单位时间内流出单位面积的质量可以通过一阶泰勒展开式求出：$\rho u + \frac{\partial \rho u}{\partial x} dx$。同样的，立方体右侧的面积为$dydz$，因此单位时间内流出流体微团的质量为:
$$
(\rho u+\frac{\partial \rho u}{\partial x}dx)dydz
$$
综合无穷小微团单位时间内流入的质量与单位时间内流出的质量，此时可以得到单位时间内$x$方向的净质量变化率为:
$$
\rho udydz-(\rho u+\frac{\partial \rho u}{\partial x}dx)dydz=-\frac{\partial \rho u}{\partial x}dxdydz
$$
同理，可得$y$方向的净质量变化率为:
$$
-\frac{\partial \rho v}{\partial y}dxdydz
$$
$z$方向的净质量变化率为:
$$
-\frac{\partial \rho w}{\partial z}dxdydz
$$
将各个方向的质量变化率相加得：
$$
-\frac{\partial \rho u}{\partial x}dxdydz-\frac{\partial \rho v}{\partial y}dxdydz-\frac{\partial \rho w}{\partial z}dxdydz=-(\frac{\partial \rho u}{\partial x}+\frac{\partial \rho v}{\partial y}+\frac{\partial \rho w}{\partial z})dxdydz
$$
结合开始根据质量变化率推导得到的方程有：
$$
\frac{\partial \rho}{\partial t}dxdydz=-(\frac{\partial \rho u}{\partial x}+\frac{\partial \rho v}{\partial y}+\frac{\partial \rho w}{\partial z})dxdydz
$$
进一步整理，得到在固定流体微团状态下的连续方程为:
$$
\frac{\partial \rho}{\partial t}+\frac{\partial \rho u}{\partial x}+\frac{\partial \rho v}{\partial y}+\frac{\partial \rho w}{\partial z}=0
$$


### 二、随流体运动的无穷小流体微团连续方程的推导

下面主要考虑随流体运动的无穷小流体微团。这个微团有固定的质量，但是它的形状和体积会在移动过程中发生改变。这里将流体微团固定的质量以及可变的体积分别用$\delta m$和$\delta V$表示,此时有：
$$
\delta m=\rho \delta V
$$
因为在流体微团运动的整个过程中质量是守恒的，因此其质量变化对时间的变化率为零，这里根据物质导数的定义，我们可以得到:
$$
\frac{D(\delta m)}{Dt}=0
$$
结合上述方程，可进一步得到:
$$
\frac{D(\rho \delta V)}{Dt}=\delta V \frac{D \rho}{D t}+\rho \frac{D(\delta V)}{Dt}
$$
可以进一步的化简为：
$$
\frac{D \rho}{D t}+\rho [\frac{1}{\delta V} \frac{D(\delta V)}{Dt}]=0
$$
上述中的第二项表示的就是速度散度，表示的是每单位体积运动着的流体微团，体积相对于变化的时间变化率，即可得到：
$$
\frac{D \rho}{Dt}+\rho \nabla.V=0
$$





