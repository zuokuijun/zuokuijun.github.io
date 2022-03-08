# conda 的安装与环境配置



### 1、Linux系统下Anaconda的安装

```lua
--下载
wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
wget -c https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh
--给执行权限
 chmod 775 Anaconda3-2020.11-Linux-x86_64.sh
--执行安装过程--安装过程中要选yes 和按下enter ，常规操作 
bash Anaconda3-2020.11-Linux-x86_64.sh #运行
--安装完成后
关闭终端，然后再打开终端以使安装后的Anaconda启动。
-- 验证是否安装成功，重新打开的终端输入以下命令
conda --version

-- 创建conda 环境 
conda create -n  [name]
-- 激活conda 环境
conda  activate [name]
-- 在conda环境中安装相应的包
conda  install  [package name]
-- 退出conda环境

```

### 2、在conda环境下安装的jupyter notebook

```lua
--在conda环境下安装jupyter notebook
conda install jupyter
--安装后在终端中输入以下命令启动：
jupyter notebook
--or 
jupyter-notebook
```



### 3、pip命令使用阿里云镜像下载安装包

```python
pip     install     [具体的包名]    -i  https://mirrors.aliyun.com/pypi/simple/ 
```

