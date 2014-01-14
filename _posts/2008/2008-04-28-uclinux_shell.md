---
layout: post
title: uClinux下的shell(Busybox) 
date: 2008-04-28 11:52:14
categories:
- 日志
tags:
- ARM
- Linux
---
### **uClinux下的shell** ###

uClinux操作系统是标准Linux的一个分支，是专门针对没有MMU(存储管理单元)的CPU而配制的操作系统，并且专为嵌入式系统做了许多小型化的工作。目前uClinux常用的应用程序库是mC-libc和mClibc。

通过make menuconfig来配置uClinux时，可以看到，这里可供选择的Shell有：*sash、minix -shell、nwsh、bash、Other。*

1. sash对应的代码为uClinux-Samsung/user/sash。
2. minix-shell对应的代码为uClinux-Samsung /user/sh。
3. nwsh对应的代码为uClinux-Samsung/user/nwsh。
4. bash对应的代码为uClinux-Samsung /user/bash。
5. Other则表示可选择其它的Shell，主要是指Busybox里面的几个Shell。

其中:

- minix-shell在mClibc和mClibc下都可以编译通过，且都可以较好地使用，但功能不是很强；
- nwsh在mC-libc和mClibc下都可以编译通过，但都工作不正常，无法进入命令行提示符；
- bash则无论在mC-libc还是mClibc下都无法编译通过，其结构不适合uClinux。本文主要讨论如何使用 Busybox中的Shell。

### **Busybox中的shell** ###

Busybox最早为Debian Linux的安装盘所写，并将大量Linux下的工具集成到一个可执行文件中。目前Busybox提供了100多个命令的功能，但它的可执行文件只有几百 KB，为嵌入式系统提供了一个比较完整而且体积较小的POSIX运行环境。不过这些命令的参数选项要比原来完整的GNU命令少。 
Busybox中集成进去的Shell有以下几个。

1. Lash：很小,加起来有10k,非常适合执行命令，支持管道和重定向，但不支持Bourne Shell语法，无法解释脚本。
2. Hush：也非常小， 18k左右，支持Bourne Shell语法，能够很好地处理if/then/else/fi结构语句，但是处理不了像for/do/done或者case/esac等循环语句。
3. Msh：加起来有30k左右，能够处理for/do/done、case/esac等循环语句。只要是Bourne shell能够做的，Msh一般都能做到，它的语法与Bourne Shell语法可能不完全相同，但大多数Bourne Shell语法都能被Msh解释。Msh是用vfork来创建新进程的，所以适于uClinux操作系统。
4. Ash：在默认配置下大约有60k左右，是 Busybox里最完整的Shell，但无法在uClinux 上编译通过。

**综上所述，Busybox里的Msh是目前uClinux下最好的Shell。**


### **移植：** ###

    make menuconfig

重新配置uClinux内核。配置时选掉sash，然后选中以下几项：

    BusyBox
    shell
    msh: Minix shell
    MSH is /bin/sh

去掉sash后，就必须在Busybox里面把原来sash下常用的一些内部命令编译进来，例如ls、cp 等基本命令，这些原来是sash的内部命令，现在换了Shell，就必须选用Busybox里面的命令作为独立的小应用程序来使用。本文中选择了以下的常用命令：clear、mkdir、ping、cat、cp、ln、ls、ifconfig等，其中的ls和ifconfig命令下面的几项功能需要全部选择。
编译的时候有个错误，是指msh.c中没有_NSIG这个定义，须在msh.c中加上这样一句：#define _NSIG 255，之后可编译通过。

编译后，在uClinux-Samsung\user\busybox目录下编译出一个单个的独立执行程序，叫做 busybox.exe。将编译后的busybox.exe拷贝到uClinux-Samsung\romfs\home目录下，重新编译内核(不用再配置内核)。将编译好的uClinux操作系统内核下载运行，使用Busybox中的Msh Shell及各种命令。使用Busybox 也很简单，只要建一个符号链接就可以了。但是由于uClinux操作系统默认的根文件系统romfs是只读的，只有/tmp和/var两个目录下是以虚拟ram盘的方法实现的可读写目录(系统掉电后，里边保存的内容全丢失)，故在进行符号链接时必须链接到这两个可读写的目录下，例如 ln -s /bin/busybox /tmp/ls，那么，执行/tmp/ls的时候，Busybox 就会执行 ls 的功能，也会按照 ls 的方式处理命令行参数。

运行成功后，可以发现这个Shell不同于原来的sash，它的提示符为#，支持上下键翻查命令，但还不支持Tab键补齐功能。

再找到uClinux-dist/config/config.in文件进行编辑，将该文件中的

    bool 'sh: tab completion' CONFIG_USER_BUSYBOX_TAB_ COMPLETION
    bool 'sh: username completion' CONFIG_USER_BUSYBOX_USER NAME_COMPLETION
改为：

    bool 'sh: tab completion' CONFIG_USER_BUSYBOX_COMMAND_ TAB_COMPLETION
    bool 'sh: username completion' CONFIG_USER_BUSYBOX_COM MAND_USERNAME_COMPLETION

然后再

    make menuconfig

选择Busybox的Shell特性后重新编译,再下载运行，就可以实现Tab键补齐功能了。

另外还可以增加Msh Shell的其它功能，比如ls命令的以彩色显示不同属性文件的功能等，这里不再详述。

![](http://i1328.photobucket.com/albums/w532/xwlogic/github%20pages/uclinux_shell2_zps4c3c8665.jpg)