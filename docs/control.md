# 流体力学控制方程总结

>在基于连续方程、动量方程以及能量方程的基础上，总结与阐述不同流体力学场景下的力学方程，主要包括：
>
>粘性流动的纳维-斯托克斯方程(Navier-Stokes)
>
>无粘流动的欧拉方程(Euler)

###  一、粘性流动的纳维-斯托克斯方程

​		粘性流动是包括摩擦、热传导和质量扩散等输运现象的流动，这些输运现象是耗散性的，他们总是使得流体的熵增加，这里并不对质量扩散做进一步的讨论。首先是针对非定常三维可压缩粘性流动的控制方程而言：

1、连续方程

非守恒形式：
$$
\frac{\mathrm{D} \rho}{\mathrm{D} t}+\rho \nabla \cdot V=0
$$
守恒形式：
$$
\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho V)=0
$$


2、动量方程

非守恒形式：
$$
x 方向 \quad \rho \frac{\mathrm{D} u}{\mathrm{D} t}=-\frac{\partial p}{\partial x}+\frac{\partial \tau_{\mathrm{xx}}}{\partial x}+\frac{\partial \tau_{y x}}{\partial y}+\frac{\partial \tau_{z x}}{\partial z}+\rho f_{x} \\
y 方向 \quad \rho \frac{\mathrm{D} v}{\mathrm{D} t}=-\frac{\partial p}{\partial y}+\frac{\partial \tau_{x y}}{\partial x}+\frac{\partial \tau_{y y}}{\partial y}+\frac{\partial \tau_{z y}}{\partial z}+\rho f_{y} \\
z 方向 \quad \rho \frac{\mathrm{D} w}{\mathrm{D} t}=-\frac{\partial p}{\partial z}+\frac{\partial \tau_{x z}}{\partial x}+\frac{\partial \tau_{y z}}{\partial y}+\frac{\partial \tau_{zz}}{\partial z}+\rho f_{z} \\
$$
守恒形式：
$$
x 方向 \quad \frac{\partial(\rho u)}{\partial t}+\nabla \cdot(\rho u \boldsymbol{V})=-\frac{\partial p}{\partial x}+\frac{\partial \tau_{x x}}{\partial x}+\frac{\partial \tau_{y x}}{\partial y}+\frac{\partial \tau_{z x}}{\partial z}+\rho f_x, \\
y 方向 \quad \frac{\partial(\rho v)}{\partial t}+\nabla \cdot(\rho v \boldsymbol{V})=-\frac{\partial p}{\partial y}+\frac{\partial \tau_{x y}}{\partial x}+\frac{\partial \tau_{y y}}{\partial y}+\frac{\partial \tau_{z y}}{\partial z}+\rho f_{y} \\
z 方向 \quad \frac{\partial(\rho w)}{\partial t}+\nabla \cdot(\rho w \boldsymbol{V})=-\frac{\partial p}{\partial z}+\frac{\partial \tau_{x z}}{\partial x}+\frac{\partial \tau_{y z}}{\partial y}+\frac{\partial \tau_{zz}}{\partial z}+\rho f_{z}
$$


3、能量方程

非守恒形式：
$$
\begin{aligned}
\rho \frac{\mathrm{D}}{\mathrm{D} t}\left(e+\frac{V^{2}}{2}\right)=& \rho \dot{q}+\frac{\partial}{\partial x}\left(k \frac{\partial T}{\partial x}\right)+\frac{\partial}{\partial y}\left(k \frac{\partial T}{\partial y}\right)+\frac{\partial}{\partial z}\left(k \frac{\partial T}{\partial z}\right)-\frac{\partial(u p)}{\partial x}-\\
& \frac{\partial(v p)}{\partial y}-\frac{\partial(w p)}{\partial z}+\frac{\partial\left(u \tau_{x x}\right)}{\partial x}+\frac{\partial\left(u \tau_{y x}\right)}{\partial y}+\frac{\partial\left(u \tau_{z x}\right)}{\partial z}+\\
& \frac{\partial\left(v \tau_{x y}\right)}{\partial x}+\frac{\partial\left(v \tau_{y y}\right)}{\partial y}+\frac{\partial\left(u \tau_{z y}\right)}{\partial z}+\frac{\partial\left(w \tau_{x z}\right)}{\partial x}+\frac{\partial\left(w \tau_{y z}\right)}{\partial y}+\\
& \frac{\partial\left(w \tau_{z z}\right)}{\partial z}+\rho \boldsymbol{f} \cdot \boldsymbol{V}
\end{aligned}
$$
守恒形式：
$$
\begin{aligned}
& \frac{\partial}{\partial t}\left[\rho\left(e+\frac{V 2}{2}\right)\right]+\nabla \cdot\left[\rho\left(e+\frac{V 2}{2}\right) V\right] \\
=& \rho \dot{q}+\frac{\partial}{\partial x}\left(k \frac{\partial T}{\partial x}\right)+\frac{\partial}{\partial y}\left(k \frac{\partial T}{\partial y}\right)+\frac{\partial}{\partial z}\left(k \frac{\partial T}{\partial z}\right)-\frac{\partial(u p)}{\partial x}-\frac{\partial(v p)}{\partial y}-\frac{\partial(w p)}{\partial z}+\\
& \frac{\partial\left(u \tau_{x x}\right)}{\partial x}+\frac{\partial\left(u \tau_{y x}\right)}{\partial y}+\frac{\partial\left(u \tau_{z x}\right)}{\partial z}+\frac{\partial\left(v \tau_{x y}\right)}{\partial x}+\frac{\partial\left(v \tau_{y y}\right)}{\partial y}+\frac{\partial\left(u \tau_{z y}\right)}{\partial z}+\\
& \frac{\partial\left(w \tau_{x z}\right)}{\partial x}+\frac{\partial\left(w \tau_{y z}\right)}{\partial y}+\frac{\partial\left(w \tau_{z}\right)}{\partial z}+\rho \boldsymbol{f} \cdot \boldsymbol{V}
\end{aligned}
$$




### 二、无粘流动的欧拉方程

无粘流的定义忽略了耗散、粘性输运、质量扩散以及热传导的流动。将上一节方程中摩擦以及热传导的项去掉，就得到无粘流动方程。

1、连续方程

非守恒形式：
$$
\frac{\mathrm{D} \rho}{\mathrm{D} t}+\rho \nabla \cdot V=0
$$


守恒形式：
$$
\frac{\partial}{\partial t}+\nabla \cdot(\rho V)=0
$$


2、动量方程

非守恒形式：
$$
x 方向 \quad \rho \frac{\mathrm{D} u}{\mathrm{D} t}=-\frac{\partial p}{\partial x}+\rho f_{x}\\
y 方向 \quad \rho \frac{\mathrm{D} v}{\mathrm{D} t}=-\frac{\partial p}{\partial y}+\rho f_{y} \\
z 方向 \quad \rho \frac{\mathrm{D} w}{\mathrm{D} t}=-\frac{\partial p}{\partial z}+\rho f_{z}
$$


守恒形式：
$$
x 方向 \quad \frac{\partial(\rho u)}{\partial t}+\nabla \cdot(\rho u \boldsymbol{V})=-\frac{\partial p}{\partial x}+\rho f_{x} \\
y 方向 \quad \frac{\partial(\rho v)}{\partial t}+\nabla \cdot(\rho v \boldsymbol{V})=-\frac{\partial p}{\partial y}+\rho f_{y} \\
z 方向 \quad \frac{\partial(\rho w)}{\partial t}+\nabla \cdot(\rho w \boldsymbol{V})=-\frac{\partial p}{\partial z}+\rho f_{z}
$$


3、能量方程

非守恒形式：
$$
\rho \frac{\mathrm{D}}{\mathrm{D} t}\left(e+\frac{V 2}{2}\right)=\rho \dot{q}-\frac{\partial(u p)}{\partial x}-\frac{\partial(v p)}{\partial y}-\frac{\partial(w p)}{\partial z}+\rho \boldsymbol{f} \cdot \boldsymbol{V}
$$
守恒形式：
$$
\frac{\partial}{\partial t}\left[\rho\left(e+\frac{V 2}{2}\right)\right]+\nabla \cdot\left[\rho\left(e+\frac{V 2}{2}\right) V\right]=\rho \dot{q}-\frac{\partial(u p)}{\partial x}-\frac{\partial(v p)}{\partial y}-\frac{\partial(w p)}{\partial z}+\rho f \cdot V
$$


