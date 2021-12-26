# 流体力学中物质导数或者随体导数的理解

​		在流体力学里，我们会遇到温度、密度、压强等这样的**标量场**（scalar field），定义这样的一个函数，需要以空间和时间为自变量，记为$f(x,y,z,t)$ ，表示在空间坐标 $(x,y,z)$ 处和时间 t 时的物理量（温度、密度、压强等）。一个流体元在 t 时刻从位置$(x,y,z)$ 运动到了$(x+ \Delta x, y+\Delta y, z+ \Delta z)$ ，会有一个物理量的变化$\Delta f$ ，其全导数为:
$$
\Delta f = \frac{\partial f}{\partial x} \Delta x +\frac{\partial f}{\partial y} \Delta y+\frac{\partial f}{\partial z} \Delta z+ \frac{\partial f}{\partial t} \Delta t+o(\rho) \\
\rho=\sqrt{(\Delta x)^2+(\Delta y)^2+(\Delta z)^2+(\Delta t)^2}
$$
这里， $o(\rho)$ 是 $\rho \rightarrow 0$时的高阶无穷小。而坐标$x,y,z$又是关于时间$t$的函数， 两边同时除以$\Delta t$得:
$$
\frac{\Delta f}{\Delta t}=\frac{\partial f}{\partial x} \frac{\Delta x}{\Delta t}+\frac{\partial f}{\partial y} \frac{\Delta y}{\Delta t}+\frac{\partial f}{\partial z} \frac{\Delta z}{\Delta t}+\frac{o(\rho)}{\Delta t}
$$
让$\Delta t$趋向于0，差分可变为微分，可丢掉尾部的高阶无穷小：
$$
\frac{df}{dt}=\frac{\partial f}{\partial x} \frac{dx}{dt}+\frac{\partial f}{\partial y} \frac{dy}{dt}+\frac{\partial f}{\partial z} \frac{dz}{dt}+\frac{\partial f}{\partial t}
$$
**随体导数**在此时被定义——流体质点在运动时所具有的物理量对时间的全导数。在高等代数里，$\nabla$ 是一个非常方便的数学符号，一个符号配合起来可以担当三个语义——
**梯度**：作用于标量$f(x,y,z)$ ,得到矢量。
$$
gradf = \nabla f = (\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} , \frac{\partial f}{\partial z})
$$
**散度**：作用于矢量$(f_x,f_y,f_z)$ ，得到标量。
$$
div \overrightarrow{f}=\nabla.\overrightarrow f=\frac{\partial f_x}{\partial x}+\frac{\partial f_y}{\partial y} + \frac{\partial f_z}{\partial z}
$$
 **旋度**：作用于矢量$(f_x,f_y,f_z)$，得到矢量。 
$$
curl \overrightarrow f=\nabla \times \overrightarrow f=\left [ \begin{matrix}
\overrightarrow i& \overrightarrow j & \overrightarrow k\\
\frac{\partial}{\partial x}& \frac{\partial}{\partial y} & \frac{\partial}{\partial z}\\
f_x & f_y & f_z 
\end{matrix} \right ] =(\frac{\partial f_z}{\partial y}-\frac{\partial f_y}{\partial z},\frac{\partial f_x}{\partial z}-\frac{\partial f_z}{\partial x},\frac{\partial f_y}{\partial x}-\frac{\partial f_x}{\partial y})
$$
位移$\overrightarrow s=(x,y,z)$是关于时间的函数，对时间求导得到速度$\overrightarrow v=(\frac{dx}{dt},\frac{dy}{dt},\frac{dz}{dt})$ 于是，前面定义的式子记作：
$$
\frac{df}{dt}=\overrightarrow v.\nabla f+\frac{\partial f}{\partial t}
$$
中间的点是向量的点乘（dot product)运算，也叫内积。我们来分解一下这个式子。`随体导数 = 对流导数 + 当地导数`。
**对流导数**（convective derivative）也叫位变导数、迁移导数，反映了空间变化对物理量的影响。
**当地导数**（domain derivative)也叫时变导数、区域导数、局部导数，反映了时间变化对物理量的影响。

举个很贴切的例子。在你乘坐高铁的时候，车厢间的电子屏幕会显示实时的速度和温度。你可以把这块电子屏当成流体元以便理解，电子屏幕需要给出的是高铁**行驶到的地点处，当前时间点**的温度。这个温度是**行走中的**温度，它与空间和时间都有关系，单独的空间或时间都不足以描述。

如果取密度$\rho$为质点的物理量，则密度的随体导数为$\frac{d \rho}{dt}$ 。对于不可压缩的流体，质点的密度在运动过程中保持不变，所以有$\frac{d \rho}{dt}=0$。

---

​	 上面主要是从数学角度对物质导数的概念进行了梳理以及推导，下面主要从物理的角度来解释什么是物质导数？首先，我们采用沿流线运动的无穷小微团作为流动模型。如下图所示:

<p align="center">
    <img src="./images/material4.png"/>
</p>



流体微团在笛卡尔坐标系下运动，设$x,y,z$轴的单位向量分别用$i,j,k$描述，则在笛卡尔坐标系下，速度向量场可以表示为：
$$
V=u_i+v_j+w_k
$$
这里速度的$x,y,z$方向向量分别由下式给出：
$$
u=u(x,y,z,t) \\
v=u(x,y,z,t) \\
w=w(x,y,z,t)
$$
我们通常考虑非定常流场，所以$u,v,w$既是位置的函数，又是时间的函数。此外，标量密度场表示为：
$$
\rho=\rho(x,y,z,t)
$$
有了上面的定义可知，流体微团在$t_1$时刻以及$t_2$时刻的密度为分别为：
$$
\rho_1=\rho(x_1,y_1,z_1,t_1) \\
\rho_2=\rho_2(x_2,y_2,z_2,t_2)
$$
既然密度表示的是位置和时间的函数，此时当流体微团处于$t_1$点时对其做如下的泰勒级数展开：
$$
\rho_2 =\rho_1+(\frac{\partial \rho}{\partial t})_1(t_2-t_1)+(\frac{\partial \rho}{\partial x})_1(x_2-x_1)+(\frac{\partial \rho}{\partial y})(y_2-y_1)_1+(\frac{\partial \rho}{\partial z})(z_2-z_1)_1+高阶项
$$
对上述式子除以$t_2-t_1$，并且忽略高阶项，可得：
$$
\frac{\rho_2-\rho_1}{t_2-t_1}=(\frac{\partial \rho}{\partial t})_1+(\frac{\partial \rho}{\partial x})_1 \frac{x_2-x_1}{t_2-t_1}+(\frac{\partial \rho}{\partial y})_1 \frac{y_2-y_1}{t_2-t_1}+(\frac{\partial \rho}{\partial z})_1 \frac{z_2-z_1}{t_2-t_1}
$$
上述式子的左边，实际上是流体微团在从位置1处移动到位置2处的过程中，密度的平均时间变化率。当$t_2$趋近于$t_1$时，这一项变为：
$$
{\lim_{t_1 \to t_2}} \frac{\rho_2-\rho_1}{t_2-t_1}=\frac{D_\rho}{D_t}
$$
这里$\frac{D_\rho}{D_t}$表示的物理含义为流体微团在空间运动时，其密度的时间变化率。而偏导数$\frac{\partial_ \rho}{\partial_t}$表示物理含义为在任意固定位置处流场瞬时起伏导致的密度变化。

在$t_2 \to t_1$时，对公式进一步取极限：
$$
{\lim_{t_1 \to t_2}} \frac{x_2-x_1}{t_2-t_1}=u
{\lim_{t_1 \to t_2}} \frac{y_2-y_1}{t_2-t_1}=v
{\lim_{t_1 \to t_2}} \frac{w_2-w_1}{t_2-t_1}=w
$$
得到：
$$
\frac{D_\rho}{D_t}=\frac{\partial \rho}{\partial t}+u\frac{\partial \rho}{\partial x}+v\frac{\partial \rho}{\partial y}+w\frac{\partial \rho}{\partial z}
$$
从而我们可以得到笛卡尔坐标系下物质导数的表达式：
$$
\frac{D}{D_t}=\frac{\partial }{\partial t}+u\frac{\partial }{\partial x}+v\frac{\partial }{\partial y}+w\frac{\partial }{\partial z}
$$
并进一步结合笛卡尔坐标系下向量算子的定义：
$$
\nabla =i \frac{\partial}{\partial x}+j\frac{\partial}{\partial y}+k \frac{\partial}{\partial z}
$$
最终得到物质导数的定义为：
$$
\frac{D}{D_t}=\frac{\partial}{\partial t}+(V.D)
$$
这里我们需要再次强调，$\frac{D}{D_t}$表示的是物质导数，它在物理上表示的是跟踪一个运动流体微团的时间变化率；而$\frac{\partial}{\partial t}$表示的是当地导数，它在物理上表示的是固定点处的时间变化率，即为流体微团从流场中的一点运动到另外一点，由于流场空间的不均匀性而引起的时间变化率。物质导数可以应用于任何流场变量如`温度场`、`压力场`、`速度场`等。

​		举一个例子进一步加深对物质导数物理意义的理解。假设你在山里徒步旅行，由于天气炎热，正要进入一个山洞。如果洞内比洞外凉爽，当你经过洞口的时候，你会感到温度降低，这就是物质导数中的对流项表示的物理含义，即空间位置的变化导致温度的改变。此时，假设你的一个朋友向你抛过来一个雪球，恰好在你通过洞口的瞬间击中了你，当雪球击中你时，你会感到一个额外的、瞬时的温度下降，这就是物质导致中的当地项所表示的物理含义（无论你是否移动、向哪移动、是否进入山洞、被雪球击中的感觉都是一样的），因此，当你通过洞口时你感觉到的总温度的下降主要由两个部分组成，一个是你进入山洞由于空间位置的改变而引起的物质导数中对流项的改变，其次是你恰好被雪球击中时当地项的改变而引入的温度下降。这里的总温就是物质导数。

<p align="center">
    <img src="./images/material3.png"/>
</p>



详细细节请参考：[随体导数的理解](https://www.zhihu.com/question/26992291/answer/1448275421)
