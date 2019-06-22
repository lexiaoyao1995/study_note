synchronized的同步方法和synchronized(this)是同步的。并且可以调用synchronized(.class)或是静态同步方法



### 在java当中都有哪些地方应用到了CAS机制呢

1、Atomic系列类

2、lock的底层实现

3、synchronized转变为重量级锁之前，也会采用CAS机制



### CAS的缺点

1、CPU开销较大

在并发量比较高的情况下，如果许多线程反复尝试去更新某一个变量，却又一直更新不成功，会给CPU带来很大压力

2、不能保证代码块的原子性

CAS机制所保证的只是一个变量的原子性操作，而不能保证整个代码块的原子性

3、ABA问题

这是CAS机制最大问题

利用版本号可以有效解决ABA问题

AtomicStampedReference



##### java语言CAS底层如何实现的

利用unsafe提供了原子操作方法

