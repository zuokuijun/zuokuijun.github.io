# Linux下按下方向按键全部变成A、B等字母以及删除键不能使用的解决方法

* 描述

  1、在Linux 下对文本进行编辑时，使用方向按键并不会使光标移动，而是在命令行中出现A、B、C、D字母；

  2、当发现编辑错误想要删除相关文本时，发现Backspace不起作用。

* 解决方案

  使用管理员模式打开/etc/vim/vimrc.tiny文件，对其进行编辑，将文本中的**set compatible**修改为**set uncompatible**，并且在其后面加上一句**set backspace=2**,保存更改之后，就可以使用vim工具对文本进行正常编辑。

