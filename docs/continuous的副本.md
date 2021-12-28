# 连续性方程——流体微元与有限体积

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


### 三、空间位置固定的有限控制体连续方程的推导

下图为一个形状任意、大小有限的控制体。该控制体的空间位置固定，其边界为控制面，流体穿过控制面，流过固定的控制体。在控制面上，设一点的流动速度为V，表面微元的面积向量为dS。dV表示有限控制体内的一个体积微元。该控制体仍然遵守质量守恒定律，即：通过控制面S流出控制体的净质量流量=控制体内质量减少的时间变化率

<p align="center">
  <img src="./images/controlVolume.png" />
</p>

对于运动的流体其穿过任意固定表面的质量流量等于（密度）$\times$ （表面面积）$\times$（垂直于表面的速度分量）。因此，通过面积$dS$的质量流量微元为：
$$
\rho V_n dS=\rho V.dS
$$
这里假定流出控制体的方向为正，则**通过控制面流出控制体的净质量流量**为:
$$
B=\iint \limits _S \rho V.d S
$$
针对体积微元$dV$，其质量为$\rho dV$。因此控制体内总质量为:
$$
\iiint \limits_{V}\rho dV
$$
此时，控制体内质量的增加率为：
$$
\frac{\partial}{\partial t} \iiint \limits_{V} \rho d V
$$
进一步，在上述式子后面添加一个负号就可以表示**控制体内质量减少的时间变化率**：

因为前面我们讨论了：`通过控制面S流出控制体的净质量流量=控制体内质量减少的时间变化率`

从而可以得到：
$$
\iint \limits _S \rho V.d S=-\frac{\partial}{\partial t} \iiint \limits_{V} \rho d V
$$
进一步，化简：
$$
\iint \limits _S \rho V.d S+\frac{\partial}{\partial t} \iiint \limits_{V} \rho d V =0
$$
上述方程就是以固定的有限控制体为研究对象，从欧拉思想出发推导得到的连续方程。



### 四、随流体运动的有限控制体连续方程的推导

如下图所示，控制体在运动过程中，体积甚至形状会发生变化但是因为控制体是由无数个无穷小的流体微团组成的，因此根据质量守恒定律，其总质量是不变的。

<p align="center">
  <img src="./images/controlVolume2.png" />
</p>

考虑有限控制体内一无穷小的体积微元$dV$，该微元的质量为$\rho dV$，其中$\rho$表示当地密度。此时，有限控制体的总质量为:
$$
m=\iiint \limits_{V} \rho dV
$$
根据物质导数的定义，由于控制体在随流体运动过程中的质量为常数，因此其物质导数为：
$$
\frac{D}{D_t} \iiint \limits_{V}\rho dV=0
$$
上述式子就是基于流动的有限控制体推导得到的连续性方程。



