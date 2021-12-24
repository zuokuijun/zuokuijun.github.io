# 多层感知机——Multi-Layer Perceptron, MLP

>参考文献：
>
>[CSDN博主chengchaowei](https://blog.csdn.net/weixin_38347387/article/details/82936585)
>
>[飞行器智能感知与控制实验室布树辉教授](https://gitee.com/pi-lab/machinelearning_notebook/blob/master/5_nn/2-mlp_bp.ipynb)
>
>[神经网络图在线编辑](http://alexlenail.me/NN-SVG/index.html)
>
>[https://gitee.com/martin64/mnist-pytorch](https://gitee.com/martin64/mnist-pytorch)
>
>[MLP网络结构的在线演示](http://playground.tensorflow.org/#activation=relu&batchSize=13&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0.001&noise=5&networkShape=4,2&seed=0.03136&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=regression&initZero=false&hideText=false)

## 1、定义

如下图所示，典型的多层神经网络主要由三部分构成：`输入层`、`隐藏层`、`输出层`。MLP神经网络不同层之间是全连接的（全连接的意思就是：上一层的任何一个神经元与下一层的所有神经元都有连接）。第一层是输入层，包括两个神经元和截距b1，负责接收输入数据；第二层是隐含层，包括两个神经元和截距b2，它们对于外部来说是不可见的；第三层是输出层，可以从这层获取神经网络输出数据。神经网络主要有三个基本要素：权重、偏置和激活函数。

* 权重：神经元之间的连接强度由权重控制，权重的大小表示可能性的大小
* 偏置：偏置的设置是为了正确分类样本，是模型中一个重要的参数，即保证通过输入算出的输出值不能随便激活。
* 激活函数：起非线性映射的作用，其可将神经元的输出幅度限制在一定范围内，一般限制在（-1~1）或（0~1）之间。最常用的激活函数是Sigmoid函数，可将（-∞，+∞）的数映射到（0~1）的范围内。

不同神经元之间连线上标注的是相邻层神经元之间的权重，这里的激活函数选择为sigmoid函数。

<p align="center">
    <img src="./images/fcn.png"/>
</p>
sigmoid函数是一个非线性函数，值域是(0,1)。函数图像如下图所示。

<p align="center">
    <img src="./images/sigmoid.jpg"/>
</p>




sigmoid函数的数学定义为：
$$
sigmoid(x)=\frac{1}{1+e^{-x}}
$$
sigmoid函数的导数为：
$$
y=sigmoid(x)y^,=y(1-y)
$$
可以看到，sigmoid函数的导数可以用sigmoid函数自身来表示。这样，一旦计算出sigmoid函数的值，计算它的导数的值就非常方便。

## 2、正向传播

神经网络正向传播的过程比较简单，就是将数据灌入到神经网络中一层一层的不断进行计算，最终将计算结果输出，动态演示过程如下图所示。

<p align="center">
    <img src="./images/fcn.gif"/>
</p>

下面首先讲述神经网络正向传播的计算原理，然后结合具体的例子来讲解神经网络的计算过程。

神经网络实际上就是一个输入向量*x*⃗ 到输出向量*y*⃗ 的函数，即：
$$
y=f_{network}(x)
$$
神经网络正向传播的计算过程为：

* 首先将输入向量的每个元素赋值给神经网络输入层对应的神经元

* 然后根据公式$sigmoid(w^Tx)$依次向前计算每一层神经元的数值，直到最后一层输出层所有神经元的数值计算完毕为止

* 最后，将神经元所有的输出值相加计算得到神经网络的输出向量$y$

  ### **神经网络正向传播实例**

    <p align="center">
        <img src="./images/fcn2.png"/>
    </p>

  输入数据	$i_1=0.05$，$i_2=0.10$

  输出数据	$o_1=0.01$，$o_2=0.99$

  初始权重	$w_1=0.15$，$w_2=0.20$，$w_3=0.25$，$w_4=0.30$

  ​				   $w_5=0.40$，$w_6=0.45$，$w_7=0.50$，$w_8=0.55$

* **1、输入层到隐含层**
  
  计算神经元h1的输入加权和：
  $$
  net_{h1}=w_1*i_1+w_2*i_2+b_1*1 \\
  net_{h1}=0.15*0.05+0.2*0.1+0.35*1=0.3775
  $$
  

​		将`加权和`代入激活函数中进行求解（sigmoid函数）：
$$
out_{h1}=\frac{1}{1+e^{-net_{h1}}}=\frac{1}{1+e^{-0.3775}}=0.593269992
$$
​		同理，可计算得出神经元h2的输出$out_{h2}=0.596884378$

* **2、隐含层到输出层**

  ​	计算输出神经元o1和o2的值：
  $$
  net_{o1}=w_5*out_{h1}+w_6*out_{h2}+b_2*1 \\
  net_{o1}=0.4*0.59326992+0.45*0.596884378+0.6*1=1.105905967 \\
  out_{o1}=\frac{1}{1+e^{net_o1}}=\frac{1}{1+e^{-1.105905967}}=0.75136507
  $$
  同理可进一步得到$out_{o2}=0.772928465$，上述就是神经网络整个前向传播的计算过程，经过计算我们得到神经网络的两个输出数值为`[1.105905967，0.75136507]`，该数值与给出的标签数值（ground-truth）相差甚远，因此还需要进一步通过反向传播的方式`更新权重`，重新计算神经网络的输出。

## 3、反向传播

### 神经网络反向传播实例

  <p align="center">
      <img src="./images/fcn2.png"/>
  </p>

 * **1、计算总误差**

​		这里神经网络计算误差的计算是根据定义的损失函数来进行计算的。这里定义神经网络的损失函数为：
$$
E_{total}=\sum {\frac{1}{2}(target-output)^2}
$$
​		这里神经网络一共有两个输出，下面分别计算神经网络的输出$o_1$以及$o_2$的误差，神经网络总的误差为两个输出的误差总和：
$$
E_{o1}=\frac{1}{2}(target_{o1}-out_{o1})^2=\frac{1}{2}(0.01-0.75136507)^2=0.274811083 \\
E_{o2}=0.023560025  \\
E_{total}=E_{o1}+E_{o2}=0.274811083 + 0.023560025=0.298371109
$$

 * **2、隐含层到输出层的权重更新**

​		下面基于损失函数的定义，采用梯度下降法对权重进行更新：
$$
wi=w-n\frac{\partial E_{total}}{\partial w_i}
$$

<p align="center">
    <img src="./images/loss1.png"/>
</p>
​		如上图所示，如果我们要更新权重$w_5$，可根据整体误差对权重$w_5$求偏导：
$$
\frac{\partial E_{total}}{\partial w_5}=\frac{\partial E_{total}}{\partial out_{o1}}*\frac{\partial out_{o1}}{\partial net_{o1}}*\frac{\partial net_{o1}}{\partial w_5}
$$
---
$$
E_{total}=E_{out1}+E_{out2}  \\
E=\frac{1}{2}(target-out)^2  \\
out_{o1}=\frac{1}{1+e^{-net_{o1}}} \\
net_{o1}=w_5*out_{h1}+w_6*out_{h2}+b_2*1
$$
---
$$
\frac{\partial E_{total}}{\partial out_{o1}}=2*\frac{1}{2}(target_{o1}-out_{o1})^{2-1}*-1+0=-(0.01-0.75136507)=0.74136507\\
\frac{\partial out_{o1}}{\partial net_{o1}}=out_{o1}(1-out_{o1})=0.75136507(1-0.75136507)=0.186815602 \\
\frac{net_{o1}}{\partial w_5}=1*out_{h1}=0.593269992\\
\frac{\partial E_{total}}{\partial w_5}=0.74136507*0.186815602*0.593269992=0.082167041
$$
---
$$
对w_5进行更新：w_5^+=w_5-n*\frac{\partial E_{total}}{\partial w_5}=0.4-0.5*0.082167041=0.35891648
$$

$$
依次对余下的权重参数进行更新：w_6^+=0.408666186,w_7^+=0.511301270,w_8^+=0.561370121
$$
---

* **3、隐含层到隐含层的权重更新**

  <p align="center">
      <img src="./images/loss2.png" />
  </p>

  与上述参数更新过程类似，这里以更新参数w1为例:
  $$
  \frac{\partial E_{total}}{\partial w_1}=\frac{\partial E_{total}}{\partial out_{h1}}*\frac{\partial out_{h1}}{\partial net_{h1}}*\frac{\partial net_{h1}}{\partial w_1}\\
  \frac{\partial E_{total}}{\partial out_{h1}}=\frac{\partial E_{o1}}{\partial out_{h1}}+\frac{\partial E_{o2}}{\partial out_{h1}}
  $$
  首先计算$\frac{\partial E_{o1}}{\partial out_{h1}}$:
  $$
  \frac{\partial E_{o1}}{\partial out_{h1}}=\frac{\partial E_{o1}}{\partial net_{o1}}*\frac{\partial net_{o1}}{\partial out_{h1}} \\
  \frac{\partial E_{o1}}{\partial net_{o1}}=\frac{\partial E_{o1}}{\partial out_{o1}}*\frac{\partial out_{o1}}{\partial net_{o1}}=0.74136507*0.186815602=0.138498562\\
  net_{o1}=w_5*out_{h1}+w_6*out_{h2}+b_2*1 \\
  \frac{\partial net_{o1}}{\partial out_{h1}}=w_5=0.40 \\
  \frac{\partial E_{o1}}{\partial out_{h1}}=0.138498562*0.40=0.055399425
  $$
  其次计算，$\frac{\partial E_{o2}}{\partial out_{h1}}$:
  $$
  \frac{\partial E_{o2}}{\partial out_{h1}}=\frac{\partial E_{o2}}{\partial net_{o2}}*\frac{\partial net_{o2}}{\partial out_{h1}} \\
  \frac{\partial E_{o2}}{\partial net_{o2}}=\frac{\partial E_{o2}}{\partial out_{o2}}*\frac{\partial out_{o2}}{\partial net_{o2}}=-0.217071535*0.175510053=-0.03809823661\\
  net_{o1}=w_5*out_{h1}+w_6*out_{h2}+b_2*1 \\
  \frac{\partial net_{o2}}{\partial out_{h1}}=w_7=0.50 \\
  \frac{\partial E_{o2}}{\partial out_{h1}}=-0.03809823661*0.50=-0.01904911831
  $$
  从而可得：
  $$
  \frac{\partial E_{total}}{\partial out_{h1}}=\frac{\partial E_{o1}}{\partial out_{h1}}+\frac{\partial E_{o2}}{\partial out_{h1}}=0.055399425+-0.01904911831=0.03635030669
  $$
  又因为：
  $$
  \frac{\partial out_{h1}}{\partial net_{h1}}=out_{h1}*(1-out_{h1})=0.59326999*(1-0.59326999)=0.241300709
  $$
  其次，
  $$
  net_{h1}=w_1*i_1+w_2*i_2+b_1*1 \\
  \frac{\partial net_{h1}}{\partial w_1}=i_1=0.05
  $$
  最终得到参数$w_1$的更新数值：
  $$
  \frac{\partial E_{total}}{\partial w_1}=0.03635030669*0.241300709*0.05=0.000438568 \\
  w_1^+=w_1-n*\frac{\partial E_{total}}{\partial w_1}=0.149780716
  $$
  

​		同理，可依次更新权重$w_2,w_3,w_4$:
$$
w_2^+=0.19956143\\
w_3^+=0.24975114 \\
w_4^+=0.29950229
$$


## 4、代码实现

```python

import torch
import torchvision
import torch.nn as nn #import torch neural network library
import torch.nn.functional as F #import functional neural network module
from torch.utils.data import DataLoader
import matplotlib.pyplot as plt
import torch.optim as optim #import optimizer neural network module
from torch.autograd import Variable #import variable that connect to automatic differentiation

class MLPNet(torch.nn.Module):

    # 定义多层神经网络架构
    def __init__(self):
        super(MLPNet, self).__init__()  # load super class for training data
        self.fc1 = nn.Linear(784, 320)
        self.fc2 = nn.Linear(320, 50)
        self.fc3 = nn.Linear(50, 10)
        self.relu = nn.ReLU()

        # 1个epoch表示将所有数据训练一遍，这里训练数据总计60000，一个batch_size设置为1000，则60个batch_size为一个epoch周期
        self.n_epochs = 20
        # 定义网络训练的batch size
        self.batch_size_train = 1000
        # 定义网络测试的batch size
        self.batch_size_test = 1000
        # 定义网络训练的学习率
        self.learning_rate = 0.01
        # 定义网络训练的参数损失
        self.momentum = 0.5
        # self.log_interval = 10

    # 对神经网络进行前向计算
    def forward(self, x):  # feed forward
        layer1 = x.view(-1, 784)  # make it flat from 0 - 320
        layer2 = self.relu(self.fc1(layer1))  # layer2 = layer1 -> fc1 -> relu
        layer3 = self.relu(self.fc2(layer2))  # layer3 = layer2 -> fc2 -> relu
        layer4 = self.relu(self.fc3(layer3))  # layer4 = layer3 -> fc2 -> relu
        return F.log_softmax(layer4, dim=1)  # softmax activation to layer4

        # 生成MINST手写数字识别的训练以及测试数据

    def data_generate(self):
        # 下载生成训练样本数据，总计包含60000个样本，但是每次仅根据batch size的大小来取固定数量的数据来进行训练
        train_loader = torch.utils.data.DataLoader(
            torchvision.datasets.MNIST('../data/', train=True, download=False,
                                       transform=torchvision.transforms.Compose([
                                           torchvision.transforms.ToTensor(),
                                           torchvision.transforms.Normalize(
                                               (0.1307,), (0.3081,))
                                       ])),
            batch_size=self.batch_size_train, shuffle=True)
        # 下载生成测试数据，总计包含10000个样本，同样根据batch size的大小来取得固定数量的数据来进行测试
        test_loader = torch.utils.data.DataLoader(
            torchvision.datasets.MNIST('../data/', train=False, download=False,
                                       transform=torchvision.transforms.Compose([
                                           torchvision.transforms.ToTensor(),
                                           torchvision.transforms.Normalize(
                                               (0.1307,), (0.3081,))
                                       ])),
            batch_size=self.batch_size_test, shuffle=True)
        return train_loader, test_loader

    def plot_MNIST(self):
        train_loder, test_loader = self.data_generate()
        examples = enumerate(train_loder)
        batch_idx, (example_data, example_targets) = next(examples)
        # example_data  torch.Size([1000, 1, 28, 28]) 每个batch size包含测试数据的个数、通道数以及图片的大小
        # example_targets 每个数据对应的标签数值
        print(example_targets)
        print(example_data.shape)
        plt.figure()
        for i in range(6):
            # plt.subplot(231)表示把显示界面分割成2*3的网格 其中，第一个参数是行数，第二个参数是列数，第三个参数表示图形的标号。
            plt.subplot(2, 3, i + 1)
            # tight_layout会自动调整子图参数，使之填充整个图像区域
            plt.tight_layout()
            # 因为这里图像是黑白的只有一个RGB通道，因此打印数组的第二个数值为0
            plt.imshow(example_data[i][0], cmap='Greys', interpolation='none')
            plt.title("Ground Truth: {}".format(example_targets[i]))
            plt.xticks([])
            plt.yticks([])
        plt.show()

    def mlp_train(self):
        # 初始化优化器，这里的优化器为随机梯度下降优化
        optimizer = optim.SGD(self.parameters(), lr=self.learning_rate, momentum=self.momentum)
        # 获得神经网络的训练数据以及测试数据
        train_loader, test_loader = self.data_generate()
        # 遍历batch size 中的每个数据
        for epoch in range(self.n_epochs):
            model.train()
            for batch_idx, (data, label) in enumerate(train_loader):
                # print("----batchsize-----", batch_idx)
                data, label = Variable(data), Variable(label)
                # 初始化梯度优化器，将梯度清零
                optimizer.zero_grad()
                # 正向传播进行计算，得到输出的loss损失
                output = model(data)  # enter data into model, save in output
                train_loss = F.nll_loss(output, label)
                # 反向传播计算梯度
                train_loss.backward()  # compute gradient
                # 更新网络权重参数
                optimizer.step()  # update weight
                if batch_idx % 10 == 0:
                    print('Train Epochs: {}, batch size: {}, Loss: {:.6f} '.format(epoch, batch_idx, train_loss.item()))
                    # plt.figure()
                    # plt.imshow(data[batch_idx][0], cmap='Greys', interpolation='none')
                    # plt.show()
                # model.mlp_test(test_loader=test_loader)
            model.eval()  # evaluation/testing
            total = 0
            correct = 0
            for data, label in test_loader:  # separate data and label
                data, label = Variable(data, volatile=True), Variable(label)  # create torch variable and enter data and label into it
                output = model(data)  # enter data into model, save in output
                # 得到预测数值
                _, predicted = torch.max(output.data, dim=1)
                # 统计预测数据与标签数据相等的字符个数
                correct += (predicted == label).sum().item()
                # 统计总的测试数据数目
                total += label.size(0)
            print('accuracy on validate set:%d %%\n' % (100 * correct / total))
            #     test_loss += F.nll_loss(output, label, size_average=False).item()  #
            #     pred = output.data.max(1, keepdim=True)[1]  # prediction result
            #     correct += pred.eq(label.data.view_as(pred)).cpu().sum()  # if label=pred then correct++
            # test_loss /= len(test_loader.dataset)  # compute test loss
            # print('\nAverage Loss: {:.4f}, Accuracy: {:.0f}'.format(test_loss, 100. * correct / len(test_loader.dataset)))

if __name__ == '__main__':
    model = MLPNet()
    model.plot_MNIST()
    # model.mlp_train()
    # # 保存训练的模型
    # torch.save(model.state_dict(), "../MLP/MLP_trained_model.pth")




```



<p align="center">
    <img src="./images/MPL_MNIST.png"/>
</p>




