# 基于PointWise的30P30N 翼型网格划分



### 一、翼型网格数据导入

* 打开`PointWise软件`，将准备好的翼型文件通过`File > Import > Database `导入。

* 这里需要说明的是， 原始的翼型网格数据格式一般第一行为当前翼型类别名称，后面紧跟的是X Y 轴的坐标，为该数据格式Point Wise是无法识别的，需要将第一行代表翼型类别的数据修改为坐标点的**总和**。比如这里针对30P30N翼型而言，其导入的数据格式为(三段机翼，因此存在三段翼型数据)：

  `301`
  
  -0.02482	-0.04248	0
  
  0.0099	0.00247	0
  
  ... ... ... ...
  
  ... ... ... ...
  
  -0.02518	-0.04369	0
  
  -0.02482	-0.04248	0
  
  `596`
  
  0.02567	-0.0036	0
  
  0.02564	-0.00365	0
  
  ... ... ... ...
  
  ... ... ... ...

  0.39135	0.00266	0

  0.02567	-0.0036	0
  
  `306`
  
  0.48666	-6.87E-04	0
  
  0.48688	-0.00108	0
  
  ... ... ... ...
  
  ... ... ... ...
  
  0.48656	-4.99E-04	0
  
  0.48666	-6.87E-04	0
  
  导入的翼型如下图所示。
  
  <p align="center">
      <img src="./images/30p30_1.png"/>
  </p>

### 二、原始翼型网格处理

​		在下面的操作中需要熟悉以下`PointWise`的快捷键：

  * `滚轮 ：缩放`

  * `Ctrl + 按住右键移动鼠标： 旋转`

  * `Ctrl+A ：选中视图中可以被选中的所有元素`

  * `Ctrl+S ：保存`

  * `Ctrl+Z ：撤销`

  * `Ctrl+X： 剪切`

  * `Ctrl+C：复制`

  * `Ctrl+V ：粘贴`

  * `Ctrl+Q ：Split 将线、面、体分为几部分`

  * `Ctrl+J  ：Joint，将几个可以合并的线、面、体合并成一个`

  * `Ctrl+G ：设置线段端点处的Spacing，用来控制线段上节点的疏密分布`

  * `Ctrl+K  ：开始选择线来生成一个面网格`

  * `Shit + Ctrl+ K： 开始选择面来生成一个体网格`

    如下图所示，导入的翼型有些位置是不平滑的。因此需要对初始的网格做一些处理，圈选中数据拟合效果较差的机翼部位，通过`Edit > Spline & Smooth`来对机翼效果较差的部位进行拟合。

    <p align="center">
        <img src="./images/30p30_2.png" />
    </p>

    <p align="center">
        <img src="./images/30p30_3.png"/>
    </p>

### 三、翼型网格划分

* ​	选中所有的曲线，点击下图中的图标，将`Dadabase`转化为` Connector `实体

  <p align="center">
      <img src="./images/30p30_4.png"/>
  </p>

* ​    根据快捷键`Ctrl +Q `以及 `Ctrl + J `对Connector 实体进行分割或者合并

  <p align="center">
      <img src="./images/30p30_5.png"/>
  </p>

*    之后根据习惯以此对每个分割的区域进行点的分配，这里点的数量不固定只要合理即可

  <p align="center">
      <img src="./images/30p30_6.png"/>
  </p>

*  这里在分配点的过程中发现，右侧的机翼分配点不均匀，该问题主要是软件自身造成的，全部选中，按下快捷键`Ctrl +G` ，`Break Point `选项中将所有的断点删除。

  <p align="center">
      <img src="./images/30p30_7.png"/>
  </p>

   * 选中相关几何区域， 按下快捷键`Ctrl + G `调整插入点的分布，尽量使得机翼翼型两侧的数据点密集

     <p align="center">
         <img src="./images/30p30_8.png"/>
     </p>

### 四、 画出机翼远场区域

<p align="center">
    <img src="./images/30p30_9.png"/>
</p>

### 五、画出整个流场范围内的非结构化网格

`Ctrl + K`开始绘制非结构化网格，需要注意的是在正式绘制之前需要选择网格类型为非机构化网格。

<p align="center">
    <img src="./images/30p30_10.png"/>
</p>

需要保证外部流场区域的方向需要机翼周围方向应该是相反的

<p align="center">
    <img src="./images/30p30_11.png"/>
</p>

<p align="center">
    <img src="./images/30p30_12.png"/>
</p>

全部设置好之后点击应用，此时就得到一个非结构化网格

<p align="center">
    <img src="./images/30p30_13.png"/>
</p>

### 六、画出层流边界层

[point wise compute wall spacing](https://www.pointwise.com/yplus/index.html)

* `Grid > T-Rex` 添加边界层

* `Boundary Conditions` 添加边界条件，将机翼设置为`Wall，Cell Types `设置为`Triangles and Quads` ，`Full Layer`: 0，`Max Layers:` 100

  <p align="center">
      <img src="./images/30p30_14.png"/>
  </p>

* 点击初始化图标，生成边界层区域网格

<p align="center">
    <img src="./images/30p30_15.png"/>
</p>

<p align="center">
    <img src="./images/30p30_16.png"/>
</p>

* 设置网格维度、求解器，边界条件等信息

  <p align="center">
      <img src="./images/30p30_20.png"/>
  </p>

<p align="center">
    <img src="./images/30p30_18.png"/>
</p>

* 设置`CAE > set  Volume conditions ` 研究对象为流体

<p align="center">
    <img src="./images/30p30_19.png"/>
</p>

* 选择`Domains` ，然后选择`Export > CAE`
