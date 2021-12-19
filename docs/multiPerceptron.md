# 多层感知机——Multi-Layer Perceptron, MLP

>参考文献：
>
>[CSDN博主chengchaowei](https://blog.csdn.net/weixin_38347387/article/details/82936585)
>
>[飞行器智能感知与控制实验室布树辉教授](https://gitee.com/pi-lab/machinelearning_notebook/blob/master/5_nn/2-mlp_bp.ipynb)
>
>[神经网络图在线编辑](http://alexlenail.me/NN-SVG/index.html)

## 1、定义

如下图所示，典型的多层神经网络主要由三部分构成：`输入层`、`隐藏层`、`输出层`。MLP神经网络不同层之间是全连接的（全连接的意思就是：上一层的任何一个神经元与下一层的所有神经元都有连接）。第一层是输入层，包括两个神经元和截距b1；第二层是隐含层，包括两个神经元和截距b2；不同神经元之间连线上标注的是相邻层神经元之间的权重，这里的激活函数选择为sigmoid函数。

<p align="center">
    <img src="./images/fcn.png"/>
</p>

sigmoid函数是一个非线性函数，值域是(0,1)。函数图像如下图所示。

![sigmod_function](https://gitee.com/pi-lab/machinelearning_notebook/raw/master/5_nn/images/sigmod.jpg)

sigmoid函数的数学定义为：
$$
sigmoid(x)=\frac{1}{1+e^(-x)}
$$
sigmoid函数的导数为：
$$
y=sigmoid(x)y^`=y(1-y)
$$
可以看到，sigmoid函数的导数可以用sigmoid函数自身来表示。这样，一旦计算出sigmoid函数的值，计算它的导数的值就非常方便。



## 4、代码实现

```python

```







