# PyTorch——数据集准备与加载



### 1、PyTorch加载数据集

```python
# 这里定义自己的数据集，数据与标签分别在不同的文件下
import os
from PIL import Image
from torch.utils.data import Dataset
import numpy as np

class MyData(Dataset):

    def __init__(self, img_dir, label_dir):
        self.img_dir = img_dir
        self.label_dir = label_dir
        # 获取所在路径下所有图片的文件名
        self.imgs = os.listdir(self.img_dir)
        # 获取所在路径下所有标签的文件名
        self.labels = os.listdir(self.label_dir)

    # 返回图片以及对应标签名称
    def __getitem__(self, item):
        img_name = self.imgs[item]
        label_name = self.labels[item]
        img_item_path = os.path.join(self.img_dir, img_name)
        label_item_path = os.path.join(self.label_dir, label_name)
        img = Image.open(img_item_path)
        with open(file="data/train/ants_label/0013035.txt", mode='r') as test:
            label = test.read()
        return img, label

    def __len__(self):
        return len(self.imgs)

root_dir = "data/train/ants_image/"
label_dir = "data/train/ants_label/"


ants_data = MyData(root_dir, label_dir)


img, label = ants_data[1]
print(img)
img.show()
print(label)
```

### 2、TensorBoard的使用

```python
# 数据显示工具类，可以实现将数据或者图片丢入该工具类中得到数据拟合的曲线，或者在网络训练中在任意阶段得到的图像数据
from torch.utils.tensorboard import SummaryWriter
from PIL import Image
import numpy as np

writer = SummaryWriter("logs")
img_dir = "data/train/bees_image/16838648_415acd9e3f.jpg"
img = Image.open(img_dir)
img_conv = np.array(img)
# print(type(img_conv))
# print(img_conv.shape)
# 输入的图像必须是numpy array  tensor格式，原始的图像格式不能写入
writer.add_image("show-image1", img_conv, 1, dataformats="HWC")

# for i in range(100):
#     writer.add_scalar("y=x", i, i)

writer.close()
```



### 3、TransForm的使用

```python
# 该模块主要对图像进行格式、大小调整以及正则化等操作
from torchvision import transforms
from torch.utils.tensorboard import SummaryWriter
from PIL import Image

path = "data/train/bees_image/29494643_e3410f0d37.jpg"
root_img = Image.open(path)


writer = SummaryWriter("logs")
# 将图像转换为tensor格式
trans = transforms.ToTensor()
tans_img = trans(root_img)

# 对图像进行正则化
normal = transforms.Normalize([3, 0, 3], [6, 1, 3])
normailze = normal(tans_img)
writer.add_image("normailze", normailze, 2)
print(root_img.size)

# 对图像进行大小变化
trans_resize = transforms.Resize((300, 300))
trans_resize = trans_resize(root_img)
# 得到的仍然是PIL格式的，因此需要将其修改为tensor格式
print(trans_resize)
trans_resize = trans(trans_resize)
print(trans_resize)
writer.add_image("resize_image", trans_resize, 1)


trans_resize2 = transforms.Resize((800, 800))
trans_resize2 = trans_resize2(root_img)
trans_resize2 = trans(trans_resize2)
writer.add_image("resize_image", trans_resize2, 3)
writer.close()
```



### 4、数据集加载器DataLoader的使用

```python
# 选择加载官方数据集，并使用数据加载器dataloader对数据进行批量加载，最终将数据批量写入到tensorboard中
import torchvision
from torch.utils.data import DataLoader
from torch.utils.tensorboard import  SummaryWriter

transform = torchvision.transforms.Compose([
    torchvision.transforms.ToTensor()
])
train_dataSet = torchvision.datasets.CIFAR10(root="./CIFAR10/data)", train=True, transform=transform, download=True)
test_dataSet = torchvision.datasets.CIFAR10(root="./CIFAR10/data)", train=False, transform=transform, download=True)

test_loader = DataLoader(dataset=test_dataSet, batch_size=64, shuffle=True, num_workers=0, drop_last=True)

writer = SummaryWriter("log")
step=0

for data in test_loader:
    imgs, label = data
    writer.add_images("testLoader_data", imgs, step)
    step = step + 1

writer.close()
```





