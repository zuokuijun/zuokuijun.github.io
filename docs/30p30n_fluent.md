# 30P30N 翼型Fluent求解器求解过程

### 一、网格文件的加载与参数设置

* 打开fluent软件，如下图所示，在开始界面需要选择网格的维度，否则软件在加载过程中会出现相关的错误

  <p align="center">
      <img src="./images/30p30_fluent_1.png"/>
  </p>

  

* 如果格式正确，fluent将加载PointWise网格以及设置的相关边界条件

  <p align="center">
      <img src="./images/30p30_fluent_2.png"/>
  </p>

* 设置缩放因子General > Scale Mesh

  <p align="center">
      <img src="./images/30p30_fluent_3.png"/>
  </p>

* 开启能量方程 Model > Energy

  <p align="center">
      <img src="./images/30p30_fluent_4.png"/>
  </p>

* 设置气体为理想气体 Materials > Fluid > air 

  <p align="center">
      <img src="./images/30p30_fluent_5.png"/>
  </p>

* 修改边界条件，机翼周围温度设置为288.15K，设置来流速度为68m/s，设置坐标X 、Y的速度大小

  <p align="center">
      <img src="./images/30p30_fluent_6.png"/>
  </p>

* 修改参考数值

  <p align="center">
      <img src="./images/30p30_fluent_7.png"/>
  </p>

* 设置求解方法

  <p align="center">
      <img src="./images/30p30_fluent_8.png"/>
  </p>

* 设置求解过程中需要显示的曲线

  <p align="center">
      <img src="./images/30p30_fluent_9.png"/>
  </p>

* 初始化

  <p align="center">
      <img src="./images/30p30_fluent_10.png"/>
  </p>

* 求解

<p align="center">
    <img src="./images/30p30_fluent_11.png"/>
</p>



### 二、求解结果分析

<p align="center">
    <img src="./images/30p30_fluent_12.png"/>
</p>



<p align="center">
    <img src="./images/30p30_fluent_13.png"/>
</p>



<p align="center">
    <img src="./images/30p30_fluent_14.png"/>
</p>



<p align="center">
    <img src="./images/30p30_fluent_15.png"/>
</p>



<p align="center">
    <img src="./images/30p30_fluent_16.png"/>
</p>
