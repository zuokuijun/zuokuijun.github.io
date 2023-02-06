#  Linux 系统新磁盘挂载

---

【Reference】: [Linux挂载新硬盘](https://blog.csdn.net/Thebest_jack/article/details/125215448)

---

* sudo  fdisk -l    查看磁盘是否安装正确，这里我们需要挂载的硬盘名为`/dev/sdb` ，如果当前步骤不显示磁盘信息，需要检查接口是否正确连接

  <p align="center">
      <img src="./images/mount1.png" />
  </p>

  

* sudo  df -h    查看目前磁盘的挂载情况

* 格式化硬盘：  `sudo mkfs.ext4 dev/sdb`

* 创建磁盘的挂载目录： 这里挂载到/home/xxx/xxx下

* sudo  mount /dev/sdb  /home/xxx/xxx     格式：sudo mount 【/dev+磁盘名】 【文件名】

* 输入df -h命令查看磁盘的挂载情况

* 最后设置开机自动挂载硬盘

  *  sudo  vim  /etc/fstab
  * 输入： /dev/sdb   /home/xxx/xxx  ext4  defaults 0 0
  * :wq 保存退出

* 完成
