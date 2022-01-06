# 能量方程

这里仍然采用随流体运动的无穷小流体微团为研究对象推导能量方程。根据热力学第一定律，对于随流体运动的微团模型而言，其满足能量守恒定律，即：<font color=#FF0000>流体微团内能量的变化率=流入微团内的净热流量+体积力和表面力对微团做功的功率</font>

**首先来看体积力以及表面力对微团做功的功率。** 可知作用在一个运动物体上的力，对物体做功的功率等于这个力乘以速度在此力作用方向上的分量。所以作用在速度为$V$的流体微团上的体积力，做功的功率为：
$$
\rho f.V(dxdydz)
$$
对于表面力（压力加上正应力和切应力）做功的功率，只考虑作用在x方向上的力。在x方向上压力和切应力对流体微团做功的功率，等于x方向上速度的分量u乘以力（比如，在面abcd上的切应力为$\tau_{xy}dxdy$，相应的功率表示为$\mu \tau_{xy}dxdy$）。在进行推导之前，这里约定作用在x正向上的力做正功，在x负方向上的力做负功。与前面一节推导动量方程的方法类似，这里我们根据上面的推导可得到作用在面adhe以及bcgf上的压力在x方向上做功的功率为：
$$
\left[u p-\left(u p+\frac{\partial(u p)}{\partial x} \mathrm{~d} x\right)\right] \mathrm{d} y \mathrm{~d} z=-\frac{\partial(u p)}{\partial x} \mathrm{~d} x \mathrm{~d} y \mathrm{~d} z
$$
类似的，在面abcd以及面efgh上，切应力在x方向上做功的功率为：
$$
\left[\left(u \tau_{y x}+\frac{\partial\left(u \tau_{y x}\right)}{\partial y} \mathrm{~d} y\right)-u \tau_{y x}\right] \mathrm{d} x \mathrm{~d} z=\frac{\partial\left(u \tau_{y x}\right)}{\partial y} \mathrm{~d} x \mathrm{~d} y \mathrm{~d} z
$$
进一步，可推导出所有的表面力对运动流体微团做功的功率为：
$$
\left[-\frac{\partial(u p)}{\partial x}+\frac{\partial\left(u \tau_{x x}\right)}{\partial x}+\frac{\partial\left(u \tau_{y x}\right)}{\partial y}+\frac{\partial\left(u \tau_{z z}\right)}{\partial z}\right] \mathrm{d} x \mathrm{~d} y \mathrm{~d} z
$$
上述式子仅仅考虑了x方向上的表面力。接下来，再考虑y以及z方向上的表面力。最终得到体积力以及应力的合力对流体微团做功的功率总和为:
$$
\begin{aligned}
C=&\left [ -\left(\frac{\partial(u p)}{\partial x}+\frac{\partial(v p)}{\partial y}+\frac{\partial(w p)}{\partial z}\right)+\frac{\partial\left(u \tau_{x x}\right)}{\partial x}+\frac{\partial\left(u \tau_{y x}\right)}{\partial y}+\frac{\partial\left(u \tau_{z x}\right)}{\partial z}+\frac{\partial\left(v \tau_{x y}\right)}{\partial x}+\right.\\
&\left.\frac{\partial\left(v \tau_{y y}\right)}{\partial y}+\frac{\partial\left(v \tau_{z y}\right)}{\partial z}+\frac{\partial\left(w \tau_{z}\right)}{\partial x}+\frac{\partial\left(w \tau_{y z}\right)}{\partial y}+\frac{\partial\left(w \tau_{z}\right)}{\partial z}\right] \mathrm{d} x \mathrm{~d} y \mathrm{~d} z+\rho f \cdot V \mathrm{~d} x \mathrm{~d} y \mathrm{~d} z
\end{aligned}
$$
**接下来继续考虑流入微团的总热流量。**主要由两部分组成：一）来自于体积加热，如吸收或者释放的辐射热；2）由温度梯度导致的跨过表面的热输送，即热传导。定义$\dot{q}$为单位质量的体积加热率。运动微团的质量为$\rho dxdydz$，从而可以得到：
$$
微团的体积加热=\rho \dot{q}dxdydz
$$
热传导从面adhe输运给微团内的热量为$\dot{q_x}dydz$。其中$\dot{q}_x$是热传导在单位时间内通过单位面积在x方向上输运的热量。因此，经过面bcgf输运到微团外的热量是:
$$
\left[\dot{q}_{x}-\left(\dot{q}_{x}+\frac{\partial \dot{q}}{\partial x} \mathrm{~d} x\right)\right] \mathrm{d} y \mathrm{~d} z=-\frac{\partial \dot{q}_{x}}{\partial x} \mathrm{~d} x \mathrm{~d} y \mathrm{~d} z
$$
进一步，加上其他面在y,z方向上的热输运量，可以得到：
$$
\text { 热传导对流体微团的加热 }=-\left(\frac{\partial \dot{q}_{x}}{\partial x}+\frac{\partial \dot{q}_{y}}{\partial y}+\frac{\partial \dot{q}_{z}}{\partial z}\right) \mathrm{d} x \mathrm{~d} y \mathrm{~d} z
$$
综上所述，总的热量=辐射总热量+热传导热量
$$
\left[\dot{\rho q}-\left(\frac{\partial \dot{q}_{x}}{\partial x}+\frac{\partial \dot{q}_{y}}{\partial y}+\frac{\partial \dot{q}_{z}}{\partial z}\right)\right] \mathrm{d} x \mathrm{~d} y \mathrm{~d} z
$$
根据傅里叶热传导定律，热传导产生的热流与当地的温度梯度成正比，其中k为热导率。
$$
\dot{q}_{x}=-k \frac{\partial T}{\partial x} \quad \dot{q}_{y}=-k \frac{\partial T}{\partial y} \quad \dot{q}_{z}=-k \frac{\partial T}{\partial z}
$$
所以，总的能量公式可进一步推导为：
$$
B=\left[\rho \dot{q}+\frac{\partial}{\partial x}\left(k \frac{\partial T}{\partial x}\right)+\frac{\partial}{\partial y}\left(k \frac{\partial T}{\partial y}\right)+\frac{\partial}{\partial z}\left(k \frac{\partial T}{\partial z}\right)\right] \mathrm{d} x \mathrm{~d} y \mathrm{~d} z
$$
**最后讨论流体微团能量变化的时间变化率**。根据热力学第一定律中内能的物理意义：气体系统的内能就是系统内每个分子和原子能量的总和。因此，运动流体微团的能量主要有两个来源：

1） 由于分子随机运动而产生的单位质量内能$e$；

2） 流体微团平动时具有的动能。单位质量的动量为$V^2/2$

因此，运动着的流体微团既有动能又有内能，两者之和就是总能量。由于是跟随着一个运动的流体微团，单位质量的总能量变化的时间变化率由物质导数给出。微团的质量为$\rho dxdydz$，所以有：
$$
A=\rho \frac{\mathrm{D}}{\mathrm{D} t}\left(e+\frac{V^{2}}{2}\right) \mathrm{d} x \mathrm{~d} y \mathrm{~d} z
$$
综上所述，根据能量守恒定律，总的计算公式为：
$$
\begin{aligned}
\rho \frac{\mathrm{D}}{\mathrm{D} t}\left(e+\frac{V^{2}}{2}\right)=& \rho \dot{q}+\frac{\partial}{\partial x}\left(k \frac{\partial T}{\partial x}\right)+\frac{\partial}{\partial y}\left(k \frac{\partial T}{\partial y}\right)+\frac{\partial}{\partial z}\left(k \frac{\partial T}{\partial z}\right)-\\
& \frac{\partial(u p)}{\partial x}-\frac{\partial(v p)}{\partial y}-\frac{\partial(w p)}{\partial z}+\frac{\partial\left(u \tau_{x x}\right)}{\partial x}+\frac{\partial\left(u \tau_{y x}\right)}{\partial y}+\frac{\partial\left(u \tau_{z x}\right)}{\partial z}+\\
& \frac{\partial\left(v \tau_{x y}\right)}{\partial x}+\frac{\partial\left(v \tau_{y y}\right)}{\partial y}+\frac{\partial\left(v \tau_{z y}\right)}{\partial z}+\frac{\partial\left(w \tau_{x z}\right)}{\partial x}+\frac{\partial\left(w \tau_{y z}\right)}{\partial y}+\frac{\partial\left(w \tau_{z z}\right)}{\partial z}+\rho \boldsymbol{f} \cdot \boldsymbol{V}
\end{aligned}
$$
需要注意的是，上述能量方程是非守恒的。

