# Docker使用教程

* 从镜像中启动一个容器

  ```bash
  docker run -it --net=host --privileged -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /home:/home --name containergui ubuntu:16.04 bash
  ```

* 从本地环境上传文件到容器

  ```bash
  docker cp   本地文件路径    容器编号：上传文件的具体路径
  ```

* 打开已经存在容器

  ```bash
  docker ps -a  # 查看已经创建的所有容器
  docker attach  容器编号
  ```

  





