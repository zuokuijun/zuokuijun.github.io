# 感知机——Perceptron

## 1、生物学解释

心理学家唐纳德·赫布（Donald Olding Hebb）于1949年提出赫布理论，该理论能够解释人类学习过程中大脑神经元所发生的变化。赫布理论描述了突触可塑性的基本原理，即突触前神经元向突触后神经元持续重复的刺激，可导致突触传递效能的增加：

> 当细胞A的轴突足以接近以激发细胞B，并反复持续地对细胞B放电，一些生长过程或代谢变化将发生在某一个或这两个细胞内，以致A作为对B放电的细胞中的一个，导致突触传递效能的增加。

<p align="center">
  <img src="./images/perceptron1.png"/>
</p>



## 2、感知机模型

如何使用机器学习方法来实现这样一个过程呢？那么感知机就构建了一个类似的结构。通过下图可以看到：Σ这个部分表示感知机模型的一个加权求和操作。首先有一系列的输入信号，当这些输入信号被传送到细胞体，那么这个细胞体会对其进行加和操作，这个加和实际上就是我们的一个加权Σ，加权之后就会产生一个加权值，加权之后通过求和得到一个值，当这个值大于0时，或者大于某一个阈值时，那么就会产生一个输出，这样的话我们就通过一个简单的数学计算，模拟了一个神经元的感知过程，他有输入，有输出，细胞体是他中间的一个计算过程，那么这个就是我们的感知机模型。

<p align="center">
  <img src="./images/perceptron2.png"/>
</p>



假设输入空间(特征向量)为**X**⊆ℝn，输出空间为**Y**∈−1,+1。输入x∈**X** 表示实例的特征向量，对应于输入空间的点；输出y∈**Y**表示示例的类别。由输入空间到输出空间的函数为:
$$
f(x)=sign(wx+b)
$$
称为感知机。其中，参数$w$叫做权值向量，$b$称为偏置。$w·x$表示$w$和$x$的内积。$sign$为符号函数，即 
$$
f(x)=\left\{
\begin{aligned}
1 && (x>=0)\\
-1 &&(x<0)
\end{aligned}
\right.
$$
给定数据集$T=(x1,y1),(x2,y2),...(x_N,y_N)$，其中

- xi∈ℝ_n
- yi∈−1,+1，i=1,2...N

感知机$sign(w·x+b)$学习的损失函数定义为

$L(w,b)=−∑yi(w⋅xi+b)$

显然，损失函数$L(w,b)$是非负的。

- 如果没有误分类点，那么$L(w,b)$为0
- 误分类点数越少，$L(w,b)$值越小

该损失函数在误分类时是参数$w,b$的线性函数，在正确分类时该损失函数是0。因此，给定训练数据集$T$，损失函数$L(w,b)$是$w,b$的连续可导函数。

## 3、算法计算步骤

**输入：**

- $T=(x1,y1),(x2,y2),...,(x_N,y_N)$, 其中xi∈**X**=ℝn，
- yi∈**Y**=−1,+1，i=1,2...N，
- 学习速率为η

**输出：**

- w, b;
- 感知机模型$f(x)=sign(w·x+b)$

**处理过程:**

1. 初始化$w_0,b_0$

2. 在训练数据集中选取$(xi,yi)$

3. 如果$yi(w∗xi+b)≤0$，即当前的样本为误分类的样本，则更新权重参数

   $w=w+ηyixi$

   $b=b+ηyi$

4. 如果所有的样本都正确分类，或者迭代次数超过设定值，则终止

5. 否则，跳转至（2）

## 4、代码实现

```python
"""
感知机_perceptron
"""

# -*- coding:utf-8 -*-
import numpy as np
import matplotlib.pyplot as plt


# 定义感知机类：里面包含数据生成、数据训练、数据测试函数
class perception_machine:
    # 随机数据生成
    def data_generate(self):
        # data generation
        # 用于生成指定随机数
        # 1、不调用seed()函数，每次随机生成的数组均不同
        # 2、调用seed()函数，若每次随机生成数组前均调用则每次生成的随机数均相同，
        #    若只调用一次，则每次生成的数值不同，但是生成的随机数值为定值
        # 比如 np.random.seed(1)
        #     np.random.randn(3, 3)
        #     np.random.seed(1)
        #     np.random.randn(3,3)
        np.random.seed(3)

        # 定义类别属于-1的10个点
        data_size1 = 10
        x1 = np.random.randn(data_size1, 2) + np.array([2, 2])
        y1 = [-1 for _ in range(data_size1)]

        # 定义类比属于1的10个点
        data_size2 = 10
        x2 = np.random.randn(data_size2, 2) * 2 + np.array([8, 8])
        y2 = [1 for _ in range(data_size2)]

        # all sample data
        # 对定义的两类数组的数据以及数据类型数组进行拼接
        x = np.concatenate((x1, x2), axis=0)
        y = np.concatenate((y1, y2), axis=0)

        # 获得随机排列的数组下标，便于从生成的数据中选取随机数据
        shuffled_index = np.random.permutation(data_size1 + data_size2)
        x = x[shuffled_index]
        y = y[shuffled_index]

        # np.newaxis的作为是增加一个矩阵维度，最终获得随机数据点以及对应的类别
        # axis=1表示对矩阵的行进行拼接
        train_data = np.concatenate((x, y[:, np.newaxis]), axis=1)

        # plot data distribution
        # plt.scatter(train_data[:, 0], train_data[:, 1], c=train_data[:, 2], marker='o')
        # plt.title("database")
        # plt.show()
        return train_data

    # 符号函数
    def sign(self, v):
        if v > 0:
            return 1
        else:
            return -1

    # 感知机训练
    def perceptron_train(self, train_data, eta=0.5, n_iter=100):
        weight = [0, 0]  # 权重
        bias = 0  # 偏置量
        learning_rate = eta  # 学习速率

        train_num = n_iter  # 迭代次数

        for i in range(train_num):
            # Random select one data
            ti = np.random.randint(len(train_data))
            (x1, x2, y) = train_data[ti]

            y_pred = self.sign(weight[0] * x1 + weight[1] * x2 + bias)

            if y * y_pred <= 0:  # 判断误分类点
                # 权重的更新为梯度的下降方向
                weight[0] = weight[0] + learning_rate * y * x1  # 更新权重
                weight[1] = weight[1] + learning_rate * y * x2
                bias = bias + learning_rate * y  # 更新偏置量
                print("update weight/bias: ", weight[0], weight[1], bias)

        return weight, bias

    # 感知机预测
    def perceptron_pred(self, data, w, b):
        y_pred = []
        for i in data:
            x1, x2, y = i
            yi = self.sign(w[0] * x1 + w[1] * x2 + b)
            y_pred.append(yi)

        return np.array(y_pred, dtype=float)


if __name__ == '__main__':
    perception = perception_machine()
    # 获得训练的数据集
    train_date = perception.data_generate()
    # 感知机训练获得权重参数以及偏置
    print("perceptron training... ...")
    w, b = perception.perceptron_train(train_date)
    print("perceptron train ending!")
    print("perceptron weigh is", w)
    print("perception bias is ", b)
    y_pre = perception.perceptron_pred(train_date, w, b)
    print("ground-truth data is ", train_date[:, 2])
    print("prediction result is", y_pre)


```







