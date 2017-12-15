### erlang/OTP

使用erlang作为开发语言已经有三年多了（之前一直使用C语言），最近想写点什么，总结一下过去几年使用erlang的心得。最近一直在思考一个问题，为什么互联网公司对服务器端的高性能高并发需求旺盛，而天生分布式的erlang语言却无人问津。可能无互联网背景的爱立信公司缺乏对erlang语言的推广，也可能erlang的开源项目较少，阻碍了erlang语言的开发和使用。这么简单强大的语言被忽视，很可惜。在此向大家强烈推荐啊^-^.

### erlang/OTP的重要特性

- 并发分布式编程

并发对于软件开发者并不陌生，采用的语言不同，需要处理问题的复杂度也不同，C/JAVA语言线程之间有很多共享内存的并发活动，处理不好会有很多互相踩脚的机会。而erlang进程拥有自己独立的内存空间和自己的信箱，其中信箱勇于存放外来的消息。与C/JAVA线程相比，erlang进程更加安全，不必担心其他进程出其不意的篡改自己的数据。erlang进程之间，是通过消息传递来通信的，接收进程会得到一份独立的数据副本，发送方感受不到接收方对副本所做的任何操作。接收方告知发送方数据的状态也是通过消息的传递。这样的进程通信方式，使得分布式计算成为可能。对于采用erlang开发的软件。部署分布式系统。不需要任何代码改动。进程之间相互隔离也给erlang的容错机制带来好处。

- 容错

erlang的哲学——“鼓励崩溃”，为了有效处理有缺陷的代码和数据，防止系统在遭遇突发状况时土崩瓦解，erlang有一套可以有效处理进程故障的进程链接系统，当一个进程异常退出时会产生一个退出信号，所有与此进程相连的进程都会收到这个信号，在默认情况下，链接进程会一并退出，直到级联在一起进程全部退出，这样保证系统不会残留未能完全关闭的进程。当然也可以设置某些相链接的进程为系统进程，只接收濒死进程的退出信号，而不退出。这种进程被称为监督者。监督者可用于汇报故障和重启子系统。

- erlang虚拟机和运行时系统

erlang进程的高效运行离不开erlang运行时系统（ERTS），这块是用C语言编写的代码，负责erlang与文件系统，终端，硬件资源打交道。ERTS包括一个重要的部分elang的虚拟机模拟器（BEAM），它非常高效，负责讲erlang程序编译成机器编码。ERTS包含了三个重要方面：
1.调度器  ---- 处理erlang进程，使得所有就绪的进程共享可用的CPU资源
2.I/O模型  ---- 防止系统进程与外部设备通信阻塞，保证系统稳定
3.垃圾回收器 ---- 回收不在使用的内存

- erlang的核心函数式语言

erlang函数式的核心是将函数看作是整数和字符串一样的数据，去匹配，匹配中了即调用，不会有while、for这样的循环计算。erlang主要借鉴了prolog语言的语法，虽然对于刚接触erlang语言的人来说，异于常规，但是忍上一段时间。你会发现，不管是代码开发速度，还是阅读速度都会提高很多。

