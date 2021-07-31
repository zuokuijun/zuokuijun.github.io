# pip 下载包时将镜像修改为国内镜像实现加速下载

* 设置超时时间

  ```c++
  pip --default-timeout=1000 install  django
  ```

* 切换国内的镜像源

   1、临时修改
  
  ​      使用pip的时候在后面加上-i参数，指定pip源　
  
   ```c++
  pip install -i https://pypi.douban.com/simple django
   ```
  
   2、永久修改
  
  ```c++
  pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
  ```
  
  
  
  

