## 0x00 梗概
目前整个操作系统项目已经完全结束，大伙可以通过此项目来深入了解操作系统层次方面的细节，这为从事系统底层工作有一定的帮助，这一个多月以来碰到过许多问题，其中让我头疼的就是PF异常，也就是page Fault异常，相反那些并不是怎么熟悉的时钟中断控制器等硬件的理解我倒是十分顺畅，这个页每次报错我就只能回头来看页面分配以及内存管理的代码，有一次甚至将代码追查到保护模式最开始建立页目录以及页表的汇编代码，最后检查出来是页目录项和页表项中低12位其中的一个访问位写错，导致用户无法正常访问页面，找出这个问题还真是让我头疼了好几天，刚好那几天还在过年，真的让我过年也过不安逸

但是最后好在还是成功实现了，功能也算比较完善，当然也可以往里面增加咱们自定义的一些系统调用，在以后如果想实现了就紧接着实现。如果有同学也想获取一个项目来锻炼自己，并且是从事底层工作的同学，其实也可以拿该项目来练练手。

我在之前学习内核pwn的过程中，由于学到了KPTI就把我搞劝退了，我想什么叫都映射在同一块，这映射在同一块是怎么实现的？就这么一点我当时硬是理解的不透彻，更不必说后面的漏洞利用了，即使我之前已经学过书本上的操作系统页表分配或映射的知识了（自我感觉应试部分还行哈，不是装杯，这是事实！）还是不理解，但是在实现了整个操作系统之后，对于这些知识确实通透了。

因此之后的工作还是接着学习安全的知识，然后如果学习的进度较快还想着能不能复现一下以前真实存在的漏洞，因为本来就是奔着二进制安全去的，操作系统是为之后学习所做的铺垫，顺便也锻炼一下自己的基本功。

---
 
## 0x01 如何使用本项目
由于这是个阶段性项目，所以我是按照自己博客中的阶段来创建分支，大家可以从自己的阶段来判断切换哪个分支查看源码
可以通过branch转换分支，我每一章都新建一个分支，方便大家不同阶段来查看，就比如当前是main分支，我们只需要点击切换即可
![](http://imgsrc.baidu.com/forum/pic/item/3ac79f3df8dcd1003d523ae5378b4710b8122f2c.jpg)

当然大伙也可以fork了本项目然后到本地用git进行切换

---
## 0x02 分支名索引
在这里给出分支及其对应进度，这样大伙可以按照自身情况来查看源码
> 0x00 环境准备 ，对应分支名-master
   
> 0x01 BIOS以及简易MBR ， 对应分支名-BIOS

> 0x02 改进版MBR，利用显卡实现输出，对应分支名-UMBR

> 0x03 加强版MBR，通过读取硬盘来加载Loader，对应分支名-UUMBR

> 0x04 进入保护模式，介绍了一些基础知识和如何进入的方法，对应分支名-Protector

> 0x05 检测内存容量，介绍如何检测的三种方法，简单易懂，对应分支名-Checkout

> 0x06 实现内存分页机制，这里是二级页表，实现了页目录表和页表，对应分支名-Page

> 0x07 载入初始内核，详细介绍特权级知识， 对应分支名-Kernel

> 0x08 实现自己的打印函数，可支持字符串，字符，整数，对应分支名-Print

> 0x09 实现了传说中的中断，重点介绍了时钟中断，对应分支名-Interrupt

> 0x0A 初步实现了内存管理机制，代码较多，对应分支名-Memory

> 0x0B 实现了内核多线程机制，对应分支名为-Thread

> 0x0C 实现了包含锁的输入输出机制，对应分支名为-IOsys

> 0x0D 实现了用户进程及其调度，对应分支名为-User

> 0x0E 实现了多种系统调用，对应分支名为-Syscall

> 0x0F 实现了硬盘分区并得到关键数据，对应分支名为-Disk

> 0x10 将文件系统初始化，并且挂载了分区，对应分支名为-FileSys_0

> 0x11 实现了几个基本的文件操作函数，对应分支名-FileSys_1

> 0x12 完善了一些文件系统功能函数，对应分支名-FileSys_2

> 0x13 文件系统真正结束，实现基本功能如ls、cd等，对应分支名-FileSys_3

> 0x14 实现简单shell且与用户交互，对应分支名-Interaction

> 0x15 实现了用户程序在虚拟机上执行以及管道的应用，对应分支名-Process
