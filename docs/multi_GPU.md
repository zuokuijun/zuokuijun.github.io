# 单机多卡并行训练策略

参考：[pytorch单机多卡训练 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/510718081)

最近在训练翼型的流场数据，之前对于1000个流场的训练基本一张卡就能搞定，但是随着数据的增加，目前大约有10000个流场数据，训练的时间周期越来越长，因此考虑采用多卡并行的方式来加速神经网络的训练速度。

显卡为RTX3090，数目为4，在单个工作站上运行训练任务

**代码实现**

```python
# 神经网络训练初始化，主要设置训练的并行通讯方式
import os
import torch.distributed as dist

local_rank = int(os.environ["LOCAL_RANK"]) # 获取当前机器支持几个GPU设备
### 设置GPU之间通信使用的后端和端口
torch.cuda.set_device(local_rank)

dist.init_process_group(backend='nccl',
                       init_method='env://')
device = torch.device(f"cuda:{local_rank}")

## 设置数据加载的采样器
train_data = MyData("./data/training_dataset", 10)
train_sampler = torch.utils.data.distributed.DistributedSampler(train_data)
train_loader = DataLoader(dataset=train_data, batch_size=batchSize, shuffle=False, sampler=train_sampler)

model = torch.nn.parallel.DistributedDataParallel(model.to(device),
                                                 device_ids=[local_rank],
                                                 out_device=local_rank)
```



**代码启动**

```python
OMP_NUM_THREADS=12 torchrun --standalone --nnodes=1 --nproc_per_node=4  train_file.py 

```





