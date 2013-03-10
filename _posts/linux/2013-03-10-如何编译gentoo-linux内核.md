---
layout: post
title: 编译gentoo linux内核 3.7.10
category : linux
tags : [linux,gentoo,kernel]
---
{% include JB/setup %}

已经不是第一次编译内核了。  
前几次都是使用iso启动，chroot后进行编译，解决不能启动的问题。   
今天更新系统后，发现有新的gentoo-source可以用。进入/usr/src目录下，发现两份源码  
linux-3.7.9-gentoo linux-3.7.10-gentoo  
linux符号链接文件则指向linux-3.7.9-gentoo目录。  
编译内核并不神秘，无非是使用编译器对源码进行编译，再使用链接器进行连接的过程。较为棘手的怕是对内核选项的配置。然而在拥有图形化展示和必要说明的配置界面下，不会造成很大的困难。具体过程如下：  
1. 修改linux符号链接使其指向最新源代码
   ln -s -T /usr/src/linux-3.7.10-gentoo /usr/src/linux
2. 进入源码目录
   cd /usr/src/linux
3. 可选。将以前的内核配置文件复制到/usr/src/linux中
   cp /usr/src/linux-3.7.{9,10}-gentoo/.config
4. 配置内核编译选项
   make menuconfig
5. 编译
   make && make modules_install
6. 拷贝新编译的内核到/boot目录下
   cp arch/x86_64/boot/bzImage /boot/kernel-3.7.10-gentoo
7. 修改grub将新内核加入启动菜单，grub2只需要重新生成grub.cfg
   grub2-mkconfig -o /boot/grub2/grub.cfg
   之前的grub修改/boot/grub.conf即可
8. 重新启动，应该可以看见新内核已经可选

   