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



### 7、神经网络实战

```python
# -*- coding: utf-8 -*-
# @Time    : 2022/1/11 11:31 下午
# @Author  : zuokuijun
# @Email   : zuokuijun13@163.com

import  torch
import  torchvision
from  torch.utils.data  import DataLoader
from  torch import  nn
from model import *
from torch.utils.tensorboard import SummaryWriter


transform = torchvision.transforms.Compose([
    torchvision.transforms.ToTensor()
])
# 训练数据集
train_data = torchvision.datasets.CIFAR10("../CIFAR10/data", train=True, download=True,transform=transform)
# 测试数据集
test_data = torchvision.datasets.CIFAR10("../CIFAR10/data", train=False, download=True, transform=transform)

test_len = len(test_data)
train_loader = DataLoader(train_data, batch_size=64)
test_loader = DataLoader(test_data, batch_size=64)

# 判断当前机器是否支持GPU训练




cnn = model()

train_step = 0
test_step = 0

epoch = 10

# 定义损失函数
if torch.cuda.is_available():
    loss = nn.CrossEntropyLoss().cuda()
else:
    loss = nn.CrossEntropyLoss()

# 定义优化器
optim = torch.optim.SGD(cnn.parameters(), lr=0.01)
writer = SummaryWriter("train_model")
for i in range(epoch):
    print("---------------------开始第{}轮网络训练-----------------".format(i+1))
    for data in train_loader:
        imgs, target = data
        if torch.cuda.is_available():
           imgs = imgs.cuda()
           target = target.cuda()
        output = cnn(imgs)
        target_loss = loss(output, target)
        optim.zero_grad()
        target_loss.backward()
        optim.step()
        train_step = train_step+1
        # 每一百步打印loss
        if train_step % 100 == 0:
            print("神经网络训练次数[{}], Loss:{}".format(train_step, target_loss.item()))
            # 绘制训练神经网络时的损失函数变化曲线
            writer.add_scalar("train_loss", target_loss.item(), train_step)

    # 一个epoch训练结束，对模型进行测试
    test_total_loss =0
    test_accuracy = 0
    with torch.no_grad():
        for data in  test_loader:
            imgs,target = data
            if torch.cuda.is_available():
                imgs = imgs.cuda()
                target = target.cuda()
            output = cnn(imgs)
            test_loss = loss(output, target)
            # 计算测试数据集整体的一个损失
            test_total_loss = test_total_loss + test_loss.item()
            # 计算测试数据集上的正确数值的个数
            accuracy = (output.argmax(1) == target).sum()
            test_accuracy = test_accuracy + accuracy

    print("测试数据集上的Loss:{}".format(test_total_loss))
    writer.add_scalar("test_loss", test_total_loss, test_step)

    print("测试数据集上的acc:{}".format(test_accuracy/test_len))
    writer.add_scalar("test_accuracy" , test_accuracy/test_len, test_step)
    test_step = test_step + 1
    torch.save(cnn, "cnn_train_{}.pth".format(i))
    print("模型已保存！")


writer.close()
```



### 8、利用GPU训练神经网络的几种设置方法

* 一般来说，需要设置的地方主要有三处：模型、损失函数以及数据

* 单GPU 模型训练以及CPU下模型的加载方式

  ### 单GPU模型训练

  ```python
  # 定义cuda设备--可以根据当前设备是否支持GPU自动选择模型、损失函数以及数据需要加载的设备类型
  device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
  # 指定模型需要加载的设备类型
  model.to(device)
  # 指定损失函数需要加载的设备类型
  loss = nn.MESLoss()
  loss = loss.to(device)
  # 指定数据需要加载的设备类型
  imgs =  imgs.to(device)
  ```
 ###        CPU模型加载
  ```python
  model = torch.load("CNN_FCN_Adam1000.pth", map_location=torch.device('cpu'))
  ```

  

* 多GPU 模型训练以及CPU下模型的加载方式 

  ### 多GPU训练

* ```python
  # 共采用4个GPU进行模型训练
  device_ids = [0, 1, 2, 3]
  BATCH_SIZE=64
  ... ...
   train_loader = DataLoader(dataset=train_data, batch_size=BATCH_SIZE * len(device_ids), shuffle=True, num_workers=2)
  
      
   # 神经网络初始化
   cnn = model()
   # 声明所有可用设备
   cnn = torch.nn.DataParallel(cnn, device_ids=device_ids)
   # 模型放在主设备
   cnn = cnn.cuda(device=device_ids[0])
   # 数据放在主设备   
   imgs = imgs.cuda(device=device_ids[0])
   label = label.cuda(device=device_ids[0])
   
  ```

		###       CPU模型加载

```python
	# 判断当前设备是否支持GPU
    USE_CUDA = torch.cuda.is_available()
    device = torch.device("cuda" if USE_CUDA else "cpu")
	# 模型加载
    model = torch.load("cnn999.pth", map_location=torch.device('cpu'))
    # 得到真实的训练模型
    model = model.module
```



