# xv6 learning note

## Chapter 1
### P12
Q:为什么不将fork 和 exec 两个调用合并为一个更简单的调用？

A: (Suspend)

To avoid the wastefulness
of creating a duplicate process and then immediately replacing it (with exec), operating kernels optimize the implementation of fork for this use case by using virtual memory techniques such as copy-on-write (see Section 4.6).

### P14

Q:什么是IO重定向？

A: 应该是指在操作系统的进程切换之中，比如说通过fork创建子进程，子进程的输出与父进程不同，这时就需要进行IO重定向来改变IO去向

### P16
Q:关于Pipes不太懂，子进程在dup为什么要再close(p[0/1])?

A: (Suspend)dup之后返回的是与原输入同一个文件描述符，关闭通道不需要的读写文件描述符是为了进程不要堵塞

## Chapter 3
虚拟地址： 

25Unused + 27index + 12offset = 64VM

物理地址:

8Unused +  44index + 12offset = 64PM

本质上是27 virtual index 映射到 44 physical index上

### P34
Q：不太清楚KSTACK在分配每个进程的内核栈是怎么分配的，好像是按线性地址划分？还是其他方式？另外satp在工作过程中是如何切换的？这个可能需要gdb调试

A:Suspend

Q:蹦床代码到底是用来干嘛的？(trampoline)

