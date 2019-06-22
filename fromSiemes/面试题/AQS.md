### AQS  是ReentantLock的底层

### Q:谈谈对于AQS的理解

#### 1、概念

AQS  abstractQueuedSynchronizer    抽象队列 同步器

定义了一套多线程访问共享资源的同步器框架，许多同步器的实现都依赖于它，如常用的ReentrantLock Semaphore

#### 2、框架

它维护了一个volatile的int型变量state（代表共享资源）和一个fifo线程等待队列（多线程争用资源时会被阻塞进入此队列）。这里volatile是核心关键，保证了state的可见性

访问state的方式有三种

getState，setState以及compareAndSetState

AQS定义两种资源共享方式，Exclusive（独占，比如reentrantLock），和share（共享）

**自定义同步器在实现的时候只需要实现共享资源state的获取与释放方式即可，至于具体线程等待队列的维护，AQS已经在底层实现好了**

主要需要实现的方法有

1 isHeldExclusively

2 tryAcquire

3 tryRelease

4 tryAcquireShared

5 tryReleaseShared

以ReentrantLock为例，state的初始化为0，表示未锁定的状态，A线程Lock时，会调用tryAcquire独占该锁，并将state+1，此后，其他线程再tryAcquire时就会失败，直到A线程unlock到state=0,为止，其他线程才有机会获获取锁，当然在锁释放前，A线程自己是可以重复获取这个锁的，这就是可重入的概念，但要注意，获取多少次就要释放多少次，这样才能保证state是能回到零状态



**比较重要的内部方法**

acquire  其实就是lock真正执行的方法

独占模式下线程获取共享资源的顶层入口，如果获取到资源，线程直接返回，否则进入等待队列，直到获取资源位置。

Node addWaiter（Node mode）此方法用于将线程加入到等待队列队尾

Node结点是对每一个访问同步代码的线程封装，其包含了需要同步的线程本身以及线程的状态。

是否被阻塞，是否等待唤醒，是否已经被取消等