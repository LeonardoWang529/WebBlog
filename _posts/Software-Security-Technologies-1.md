---
title: Software_Security_Technologies_1
date: 2019-09-28 22:50:45
tags:
- Security Defence
categories: 'Security'
---

In this artical I will talk about our first software Security Technology -- Privilege Separation

The main idea of this is dividing the functionalities of an app to different modules. then using privilege drop and chroot to create a jail for this functionality, make it only can run the task for this module. then we use Named Pipe or FIFO to communicate between two modules.
Privilege Sepration的核心思想就和名字一样，把功能分散成不同地子线程，在把子线程的权限控制在本身所需要的范围内。理论上来说privilege separation 之后，user的privilege 没有了，只能在一个给出来的无用的地址，并且存储空间也是separated，这个 attacker就没法拿到任何数据，去到任何地址，最多只能对这个process 做一个overflow attack。但这个影响不了main process，最多就是这个process 被杀掉了。随便再想一个，如果这个app是有对外calling的，那可不可以把它作为slave 呢。答案是不一定，看你给这个对外的process多大的权限，如果这个process上的user并没有写的权限的话，那hack进来了，应该也是改不了通信地址的。


The advantage of this is only couple processes are working in the root privilege(others are working under low privilege). Even if the hacker gets into the input or output processes, due to the data address change, privilege drop and root dir change, he can not change the dirct and go anywhere. It performs like a jail, here we only can do what the code needs to do.

required linux functions and what is for:
	fork() -- Functions separation, privilege dropping. 
	exec() -- allows the OS to randomize the child’s address space
	chroot() -- Provides a restricted view of the filesystem
	setuid() -- change user droping privilege
	mkfifo() -- 

A good example is to look at is ntpd(). We first need to find what function does it need: read files(dns), set system Clocks, inital socket connection. here set system clock require privilege, we use it as the main process, other processes will be separate from there.






