# 流体力学中物质导数或者随体导数的理解

本是数学上的一个概念——**全导数**（ total derivative ），相对**偏导数**（ partial derivative ）而言。然后放到物理里特定的**流体力学**场景，给出了新名称——**物质导数**（ material derivative ）。

　　物质导数，也叫**随体导数**。不知道谁给翻译的，竟有些信达雅。“体”对应“物质”，表示该点周围很小范围内的物质，术语称**流体微团**（blob）、**流体元**（fluid element）；“随”是跟随、伴随的意思，相对静态的“物质”名称而言，有动态的感觉了。

言归正传。在流体力学里，我们会遇到温度、密度、压强等这样的**标量场**（scalar field），定义这样的一个函数，需要以空间和时间为自变量，记为 ![[公式]](https://www.zhihu.com/equation?tex=f%28x%2C+y%2C+z%2C+t%29)，表示在空间坐标 ![[公式]](https://www.zhihu.com/equation?tex=%28x%2C+y%2C+z%29) 处和时间 t 时的物理量（温度、密度、压强等）。一个流体元在 t 时刻从位置 ![[公式]](https://www.zhihu.com/equation?tex=%28x%2C+y%2C+z%29) 运动到了 ![[公式]](https://www.zhihu.com/equation?tex=%28x+%2B+%5CDelta+x%2C+y+%2B+%5CDelta+y%2C+z+%2B+%5CDelta+z%29) ，会有一个物理量的变化 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+f) ，其全导数为 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+f+%3D+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+x%7D+%5CDelta+x+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+y%7D+%5CDelta+y+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+z%7D+%5CDelta+z+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+t%7D+%5CDelta+t+%2B+o%28%5Crho%29) 。 ![[公式]](https://www.zhihu.com/equation?tex=%5Crho+%3D+%5Csqrt+%7B%28%5CDelta+x%29%5E2+%2B+%28%5CDelta+y%29%5E2+%2B+%28%5CDelta+z%29%5E2+%2B+%28%5CDelta+t%29%5E2%7D) ， ![[公式]](https://www.zhihu.com/equation?tex=o%28%5Crho%29) 是 ![[公式]](https://www.zhihu.com/equation?tex=%5Crho+%5Crightarrow+0) 时的**高阶无穷小**。而坐标x，y，z又可以是关于时间 t 的函数，两边同时除以 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+t) 得 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac+%7B%5CDelta+f%7D%7B%5CDelta+t%7D+%3D+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+x%7D+%5Cfrac+%7B%5CDelta+x%7D%7B%5CDelta+t%7D+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+y%7D+%5Cfrac+%7B%5CDelta+y%7D%7B%5CDelta+t%7D+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+z%7D+%5Cfrac+%7B%5CDelta+z%7D%7B%5CDelta+t%7D+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+t%7D+%2B+%5Cfrac+%7B+o%28%5Crho%29%7D%7B%5CDelta+t%7D) 。让 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+t) 趋近于0，差分变微分，可丢掉尾部的高阶无穷小量， ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac+%7Bdf%7D%7Bdt%7D+%3D+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+x%7D+%5Cfrac+%7Bdx%7D%7Bdt%7D+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+y%7D++%5Cfrac+%7Bdy%7D%7Bdt%7D+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+z%7D++%5Cfrac+%7Bdz%7D%7Bdt%7D+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+t%7D) 。**随体导数**在此时被定义——流体质点在运动时所具有的物理量对时间的全导数。

　　**是公式都会追求短而美**（多看看麦克斯韦方程组，你能从中领略到公式的美）。我们学的 Nabla 算子（符号 ![[公式]](https://www.zhihu.com/equation?tex=%5Cnabla) ，即倒立的 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta) ）选择在这个时候登场。在高等代数里， ![[公式]](https://www.zhihu.com/equation?tex=%5Cnabla) 是一个非常方便的数学符号，一个符号配合起来可以担当三个语义——
**梯度**：作用于标量 ![[公式]](https://www.zhihu.com/equation?tex=f%28x%2C+y%2C+z%29) ，得到矢量。 ![[公式]](https://www.zhihu.com/equation?tex=grad+f+%3D+%5Cnabla+f+%3D+%28%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+x%7D%2C+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+y%7D%2C+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+z%7D%29) 
**散度**：作用于矢量 ![[公式]](https://www.zhihu.com/equation?tex=%28f_x%2C+f_y%2C+f_z%29) ，得到标量。 ![[公式]](https://www.zhihu.com/equation?tex=div+%5Cvec+f+%3D+%5Cnabla+%5Ccdot++%5Cvec+f+%3D+%5Cfrac+%7B%5Cpartial+f_x%7D%7B%5Cpartial+x%7D+%2B+%5Cfrac+%7B%5Cpartial++f_y%7D%7B%5Cpartial+y%7D+%2B+%5Cfrac+%7B%5Cpartial++f_z%7D%7B%5Cpartial+z%7D) 
**旋度**：作用于矢量 ![[公式]](https://www.zhihu.com/equation?tex=%28f_x%2C+f_y%2C+f_z%29) ，得到矢量。 ![[公式]](https://www.zhihu.com/equation?tex=curl+%5Cvec+f+%3D+%5Cnabla+%5Ctimes++%5Cvec+f+%3D+%5Cbegin%7Bvmatrix%7D+%5Cvec+i+%26+%5Cvec+j+%26+%5Cvec+k+%5C%5C+%5Cfrac+%7B%5Cpartial%7D%7B%5Cpartial+x%7D+%26+%5Cfrac+%7B%5Cpartial%7D%7B%5Cpartial+y%7D+%26+%5Cfrac+%7B%5Cpartial%7D%7B%5Cpartial+z%7D+%5C%5C+f_x+%26+f_y+%26+f_z+%5Cend%7Bvmatrix%7D+%3D+%28%5Cfrac+%7B%5Cpartial+f_z%7D+%7B%5Cpartial+y%7D+-+%5Cfrac+%7B%5Cpartial++f_y%7D+%7B%5Cpartial+z%7D%2C+%5Cfrac+%7B%5Cpartial+f_x%7D+%7B%5Cpartial+z%7D+-+%5Cfrac+%7B%5Cpartial+f_z%7D+%7B%5Cpartial+x%7D%2C+%5Cfrac+%7B%5Cpartial+f_y%7D+%7B%5Cpartial+x%7D+-+%5Cfrac+%7B%5Cpartial+f_x%7D+%7B%5Cpartial+y%7D%29) 。
位移 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvec+s+%3D+%28x%2C+y%2C+z%29) 是关于时间的函数，对时间求导得到速度 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvec+v+%3D+%28%5Cfrac+%7Bdx%7D%7Bdt%7D%2C+%5Cfrac+%7Bdy%7D%7Bdt%7D%2C+%5Cfrac+%7Bdz%7D%7Bdt%7D%29) 。
 于是，前面定义的式子记作![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac+%7Bdf%7D%7Bdt%7D+%3D+%5Cvec+v+%5Ccdot+%5Cnabla+f+%2B+%5Cfrac+%7B%5Cpartial+f%7D%7B%5Cpartial+t%7D) 。中间的点是向量的点乘（dot product）运算，也叫内积。我们来分解一下这个式子。
随体导数 = 对流导数 + 当地导数。
**对流导数**（convective derivative）也叫位变导数、迁移导数，反映了空间变化对物理量的影响。
**当地导数**（domain derivative）也叫时变导数、区域导数、局部导数，反映了时间变化对物理量的影响。

　　举个很贴切的例子。在你乘坐高铁的时候，车厢间的电子屏幕会显示实时的速度和温度。你可以把这块电子屏当成流体元以便理解，电子屏幕需要给出的是高铁**行驶到的地点处，当前时间点**的温度。这个温度是**行走中的**温度，它与空间和时间都有关系，单独的空间或时间都不足以描述。

　　如果取密度 ![[公式]](https://www.zhihu.com/equation?tex=%5Crho) 为质点的物理量，则密度的随体导数为 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac+%7Bd%5Crho%7D+%7Bdt%7D) 。对于不可压缩的流体，质点的密度在运动过程中保持不变，所以有 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac+%7Bd%5Crho%7D+%7Bdt%7D+%3D+0) 。懂了随体导数的概念，离理解**纳维尔-斯托克斯方程**（Navier-Stokes equation）就近了一步，加油！

详细细节请参考：[随体导数的理解](https://www.zhihu.com/question/26992291/answer/1448275421)