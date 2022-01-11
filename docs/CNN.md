# 卷积神经网络——CNN

>[PyTorch官网](https://pytorch.org/docs/stable/nn.html)

## 神经网络基本组成

```python
import torch.nn as nn
import torch.nn.functional as F

# 继承Model类
class Model(nn.Module):
    def __init__(self):
        # 初始化父类
        super(Model, self).__init__()
        # 定义卷积层
        self.conv1 = nn.Conv2d(1, 20, 5)
        self.conv2 = nn.Conv2d(20, 20, 5)
	# 神经网络前向传播
    def forward(self, x):
        x = F.relu(self.conv1(x))
        return F.relu(self.conv2(x))
```



### 1、卷积层

```python
import torch
from torch import nn
import torchvision
from torch.nn import Conv2d
from torch.utils.data import  DataLoader
from torch.utils.tensorboard import  SummaryWriter

dataset = torchvision.datasets.CIFAR10("../CIFAR10/data", train= False, transform= torchvision.transforms.ToTensor(), download=True )
dataLoader = DataLoader(dataset= dataset, batch_size= 64)

class Model(nn.Module):
    def __init__(self):
        super(Model, self).__init__()
        self.conv1 = Conv2d(in_channels=3, out_channels=6, kernel_size=3, stride=1,padding=0)

    def forward(self, x):
        x = self.conv1(x)
        return  x


model = Model()

writer = SummaryWriter("cnn_test")

step = 0
for data in dataLoader:
    imgs, labels = data
    out = model(imgs)
    print(imgs.shape)
    print(out.shape)
    # torch.Size([64, 3, 32, 32])
    writer.add_images("input", imgs, global_step=step)
    # torch.Size([64, 6, 30, 30])
    out = torch.reshape(out,(-1,3,30,30))
    writer.add_images("output", out, global_step=step)
    step = step + 1

writer.close()

```

- **in_channels** ([*int*](https://docs.python.org/3/library/functions.html#int)) – Number of channels in the input image

- **out_channels** ([*int*](https://docs.python.org/3/library/functions.html#int)) – Number of channels produced by the convolution

- **kernel_size** ([*int*](https://docs.python.org/3/library/functions.html#int) *or* [*tuple*](https://docs.python.org/3/library/stdtypes.html#tuple)) – Size of the convolving kernel

- **stride** ([*int*](https://docs.python.org/3/library/functions.html#int) *or* [*tuple*](https://docs.python.org/3/library/stdtypes.html#tuple)*,* *optional*) – Stride of the convolution. Default: 1

- **padding** ([*int*](https://docs.python.org/3/library/functions.html#int)*,* [*tuple*](https://docs.python.org/3/library/stdtypes.html#tuple) *or* [*str*](https://docs.python.org/3/library/stdtypes.html#str)*,* *optional*) – Padding added to all four sides of the input. Default: 0

- **padding_mode** (*string**,* *optional*) – `'zeros'`, `'reflect'`, `'replicate'` or `'circular'`. Default: `'zeros'`

- **dilation** ([*int*](https://docs.python.org/3/library/functions.html#int) *or* [*tuple*](https://docs.python.org/3/library/stdtypes.html#tuple)*,* *optional*) – Spacing between kernel elements. Default: 1

- **groups** ([*int*](https://docs.python.org/3/library/functions.html#int)*,* *optional*) – Number of blocked connections from input channels to output channels. Default: 1

- **bias** ([*bool*](https://docs.python.org/3/library/functions.html#bool)*,* *optional*) – If `True`, adds a learnable bias to the output. Default: `True`

<p align="center">
  <img src="./images/conv_input.png"/>
</p>

  <p align="center">
    <img src="./images/conv_output.png" />
  </p>

<p align="center">
  <img src="./images/conv_calcu.png" />
</p>



### 2、池化层

```python
import torch
from torch import  nn
from torch.utils.data import  DataLoader
from torch.utils.tensorboard import  SummaryWriter
import torchvision


dataset = torchvision.datasets.CIFAR10("./CIFAR10/data", train= True, transform= torchvision.transforms.ToTensor(), download=True )
dataLoader = DataLoader(dataset= dataset, batch_size=64)

class  model(nn.Module):

    def __init__(self):
        super(model, self).__init__()
        self.max_pooling = nn.MaxPool2d(kernel_size=3, ceil_mode=True)

    def forward(self, x):
        out = self.max_pooling(x)
        return out

writer = SummaryWriter("maxpooling_test")

model = model()
step = 0
for data in dataLoader:
    imgs, label = data
    out = model(imgs)
    print(imgs.shape)
    print(out.shape)
    writer.add_images("input", imgs, global_step=step)
    writer.add_images("output", out, global_step= step)
    step = step +1

writer.close()

```

<p align="center">
  <img src="./images/pooling_input.png" />
</p>

<p align="center">
  <img src="./images/pooling_output.png" />
</p>



### 3、线性层

定义全连接神经网络

```python
m = nn.Linear(20, 30)
input = torch.randn(128, 20)
output = m(input)
print(output.size())
```



### 4、激活函数

| [Sigmoid](https://pytorch.org/docs/stable/generated/torch.nn.Sigmoid.html#torch.nn.Sigmoid) | [LeakyReLU](https://pytorch.org/docs/stable/generated/torch.nn.LeakyReLU.html#leakyrelu) | [RELU](https://pytorch.org/docs/stable/generated/torch.nn.ReLU.html#torch.nn.ReLU) | [Softmax](https://pytorch.org/docs/stable/generated/torch.nn.Softmax.html#torch.nn.Softmax) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |



### 5、损失函数

| [L1Loss](https://pytorch.org/docs/stable/generated/torch.nn.L1Loss.html#torch.nn.L1Loss) | [MSELoss](https://pytorch.org/docs/stable/generated/torch.nn.MSELoss.html#torch.nn.MSELoss) | [CrossEntropyLoss](https://pytorch.org/docs/stable/generated/torch.nn.CrossEntropyLoss.html#torch.nn.CrossEntropyLoss) | [NLLLoss](https://pytorch.org/docs/stable/generated/torch.nn.NLLLoss.html#torch.nn.NLLLoss) |
| :----------------------------------------------------------: | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |



### 6、Example

```python
# -*- coding: utf-8 -*-
# @Time    : 2022/1/11 7:46 下午
# @Author  : zuokuijun
# @Email   : zuokuijun13@163.com
import torch
from torch import nn
import torchvision
from torch.utils.tensorboard import SummaryWriter
from torch.utils.data import DataLoader

dataset = torchvision.datasets.CIFAR10("../CIFAR10/data", train= True, transform= torchvision.transforms.ToTensor(), download=True )
dataLoader = DataLoader(dataset=dataset, batch_size=64)

class model(nn.Module):
    def __init__(self):
        super(model, self).__init__()
        self.model1 = nn.Sequential(
            nn.Conv2d(in_channels=3,
                      out_channels=32,
                      kernel_size=5,
                      padding=2),
            nn.MaxPool2d(2),
            nn.Conv2d(in_channels=32,
                      out_channels=32,
                      kernel_size=5,
                      padding=2),
            nn.MaxPool2d(2),
            nn.Conv2d(in_channels=32,
                      out_channels=64,
                      kernel_size=5,
                      padding=2),
            nn.MaxPool2d(2),
            nn.Flatten(),
            nn.Linear(1024, 64),
            nn.Linear(64, 10)
        )

    def forward(self, x):
        x = self.model1(x)
        return x

model = model()
loss = nn.CrossEntropyLoss()
optimize = torch.optim.SGD(model.parameters(), lr=0.01)
for data in dataLoader:
    imgs, target = data
    output = model(imgs)
    # 利用损失函数计算神经网络的损失
    result = loss(output, target)
    print("loss", result)
    # 梯度清零
    optimize.zero_grad()
    # 反向传播更新网络参数
    result.backward()
    optimize.step()
```





