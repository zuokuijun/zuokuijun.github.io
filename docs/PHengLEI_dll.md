# PHengLEI 风雷软件运行.exe文件时报.dll文件缺失错误

## 1、 问题描述

删除电脑中的microsoft  visual studio 或者同一电脑存在两个版本的 visual studio 还有就是新的电脑即使在安装了microsoft  visual studio，在运行风雷编译后的.exe文件后依然报.dll文件缺失错误

## 2、 解决方案

[参考文献](https://blog.csdn.net/qq_44658096/article/details/126218364)
   
  * 到该网站[https://cn.dll-files.com/](https://cn.dll-files.com/)上面下载对应版本的缺失.dll文件，提示缺啥就下载啥，64以及32位的都需要下载

  * 将下载的文件进行解压，64位的文件需要放在**C:\Windows\System32**； 32位的文件放在:**C:\Windows\SysWOW64**
  
   

