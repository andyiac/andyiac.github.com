---
layout: post
category: android 
tags : [android]
title : genymotion unable to load VirtualBox engine error 
---
{% include JB/setup %}


在ubuntu 14.04 上使用 genymotion模拟器时遇到了一下问题，提示：
		
	Unable to load VirtualBox engine

Google 一番发现如下命令可顺利解决问题：

	➜  ~ virtualbox restart
	WARNING: The vboxdrv kernel module is not loaded. Either there is no module
	available for the current kernel (3.16.0-49-generic) or it failed to
	load. Please recompile the kernel module and install it by

		sudo /etc/init.d/vboxdrv setup

	You will not be able to start VMs until this problem is fixed.

根据提示重新编译 kernel 模块 

	➜  ~ sudo /etc/init.d/vboxdrv setup
	Stopping VirtualBox kernel modules ...done.
	Recompiling VirtualBox kernel modules ...done.
	Starting VirtualBox kernel modules ...done.

打完手工
