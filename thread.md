### yield

概念：

当调用Thread.yield()函数时，会给线程调度器一个当前线程愿意让出CPU使用的暗示，但是线程调度器可能会忽略这个暗示。

### 如何中断线程

目前使用的方法

调用interrupt()，，通知线程应该中断了

1、如果线程处于被阻塞状态，那么线程将立即退出被阻塞状态，并抛出一个IntertuptedException异常

2、如果线程处于正常活动状态，那么会将该线程的中断标志设置为true，被设置中断标志的线程将继续正常运行。

3、需要被调用的线程配合中断

在正常运行任务时，经常检查本线程的中断标记位，如果被设置了中断标记就自动停止线程00000

### 线程安全问题的主要诱因

1、存在共享数据

2、存在多条线程共同操作这些共享数据

解决问题的根本方法：

同一时刻有且只有一个线程在操作共享数据，其他线程必须等到该线程处理完数据后再对共享数据进行操作。

### synchronized互斥锁的特性

1、互斥性：即在同一时刻只允许一个线程持有某个对象锁，通过这种特性来实现多线程的协调机制，这样在同一时间只有一个线程对需要同步的代码块。互斥性页称作操作的原子性

2、可见性：必须确保在锁被释放之前，对共享变量所做的修改，对于随后获得该锁的另一个线程是可见的，否则另一个线程可能是本地缓存的某个副本上继续操作，从而引起不一致。

synchronized锁的不是代码，锁的都是对象。

### 根据获取的锁的分类：获取对象锁和获取类锁

获取对象锁的两种用法：

1、同步代码块(synchronized(this)，synchronized(类实例对象))，锁是小括号()中的实例对象

2、同步非静态方法，锁是当前对象的实例对象

获取类锁的两种方法：

1、同步代码块(synchronized(类.class))，锁是小括号（）中的类对象（Class对象）

2、同步静态方法，（synchronized static method），锁是当前对象的类对象

### 对象锁和类锁的总结

1、有线程访问对象的同步代码块，另外的线程可以访问该对象的非同步代码块

2、若锁住的是同一个对象，一个线程在访问对象的同步代码块时，另一个访问对象的同步代码块的线程会被阻塞

3、若锁住的是同一个对象，一个线程在访问对象的同步方法时，另一个访问对象同步方法的线程会被阻塞

4、若锁住的是同一个对象，一个线程在访问对象的同步代码块时，另一个访问对象同步方法的线程会被阻塞，反之亦然

5、同一个类的不同对象的对象锁互不干扰

6、类锁由于也是一中特殊的对象锁，因此表现和上述1，2，3，4一致，而由于一个类只能有一个对象锁，所以同一个类的不同对象使用类锁将会是同步的

7、类锁和对象锁互补干扰

### synchronized底层实现原理

#### 实现synchronized基础

1、java对象头

2、Monitor

#### 对象在内存中的布局

1、对象头 ，

结构包括 Mark Word ， Class Metadata Address

Mark Word 包括hashCode，分代年龄，锁类型等信息，重量级锁（指针指向的是monitor的起始地址，synchronized锁）

Class Metadata Address  类型指针指向对象的类元数据，jvm通过这个指针确定该对象是哪个类的数据

2、实例数据

3、对齐填充

### monitor

每个java对象天生自带一把看不见的锁

### synchronized是可重入锁

什么是重入

从互斥锁的设计上来说，当一个线程试图操作一个由其他线程持有的对象锁的临界资源时，将会处于阻塞状态，但是当一个线程再次请求自己持有对象锁的资源时，这种情况属于重入

### 自旋锁   PreBlockSpin

许多情况下，共享数据的锁定状态持续时间短，切换线程不值得

通过让线程执行忙循环等待锁的释放，不让出CPU

缺点：若锁被其他线程长时间占用，会带来许多性能上的开心

### 自适应自旋锁

1、自旋的次数不再固定

2、由前一次在同一个锁上的自旋时间及锁的拥有者的状态来决定

### 锁消除

**优化**

编译时，对上下文进行扫描，去除不可能存在竞争的锁

### 锁粗化

**另一种极端**

扩大加锁的范围，避免反复加锁和解锁

### synchronized的四种状态

无锁  偏向锁 轻量级锁 重量级锁

**锁降级**

**锁膨胀**

##### 偏向锁

减少同一线程获取锁的代价

大多数情况下，锁不存在多线程竞争，总是同一个线程多次获得

核心思想：

如果一个线程获得了锁，那么锁就进入偏向模式，此时mark word的结构也变为偏向锁，当该线程再次请求锁时，无需再做任何同步操作，即获取锁的过程只需要检查mark word的锁标记以及当前线程id等于mark word的threadid即可，这样就省去了大量有关锁的申请操作

不适合锁竞争激烈的场合

##### 轻量锁

轻量级锁是偏向锁升级来的，偏向锁运行在一个线程进入同步块的情况下，当第二个线程加入锁争用的时候，偏向锁就会升级为轻量锁

适用的场景：线程交替执行同步块

若存在同一时间访问同一锁的情况，就会导致轻量锁膨胀为重量锁

##### 重量级锁

使用场景：同步块执行时间较长的场景



### ReentrantLock（再入锁）

  位于java.util.concurrent.locks包

基于AQS实现

能够实现比synchronized更细粒度的控制，如fairness

调用lock后必须用unlock

性能未必比synchronized高，并且也是可重入的



##### 公平性设置

ReentrantLock fair = new ReentrantLock(true)

参数为true时，倾向于将锁赋予等待时间最久的线程

公平锁，获取锁的顺序按先后调用lock方法的顺序

非公平锁：抢占顺序不一定

synchronized是非公平锁



##### ReentrantLock将锁对象化

判断是否有线程在排队等待获取锁

带超时的获取锁的尝试

感知有没有成功获取锁 



##### wait、notify notifyAll  Condition



##### ReentrantLock和synchronized的区别

总结：

1、ReentrantLock是类，synchroized关键字

2、ReentrantLock可以对获取锁的等待时间设置，避免死锁

3、ReentrantLock可以获取各种锁的信息

4、ReentrantLock可以灵活实现多路通知

机制  synchronized操作Mark word  ReentrantLock调用unsafe类的park方法



### 指令重排序需要满足的条件

1、在单线程环境中不能改变程序运行的结果

2、存在数据依赖关系的不允许重排序

即时

**无法通过happens-before原则推导出来，才能进行指令的重排序**



### volatile ：jvm提供的轻量级同步机制

1、保证被volatile修饰的共享变量对所有线程总是可见的

2、禁止指令重排序优化



### volatile变量为何立即可见

当写一个volatile变量时，jmm会把该线程对应的工作内存中的共享变量值刷新到主内存中

当读取一个volatile变量时，jmm会把该线程对应的工作内存设置为无效



### volatile如何禁止重排优化

利用内存屏障

1、保证特定操作的执行顺序

2、保证某些变量的内存可见性

通过插入内存屏障指令禁止在内存屏障前后的指令执行排序优化



### java线程池

##### 利用Executors创建不同的线程池满足不同场景的需求

1、newFixedThreadPool（int n）

指定工作线程数量的线程池

2、newCachedThreadPool（）

处理大量短时间工作任务的线程池

（1）试图缓存线程并重用，当无缓存线程可用时，就会创建新的工作线程

（2）如果线程闲置的时间超过阈值，则会被终止并被移出缓存

（3）系统长时间闲置的时候，不会消耗资源

3、newSingleThreadExecutor（）

创建唯一的工作者线程来执行任务

4、newScheduledThreadPool

定时或周期性的工作调度

5、newWorkStealingPool

内部构建forkJoinPool，利用working-stealing算法，并行处理任务。

### 为什么要使用线程池子

1、降低资源消耗

2、提高线程的可管理性

### juc的三个executor接口

1、executor  运行新任务的简单接口，将任务提交和任务执行细节解耦

2、executorService  具备管理执行器和任务生命周期的方法，提交任务机制更完善

3、scheduledExecutorService  支持future和定期执行任务



### ThreadPoolExecutor的构造函数

1、corePoolSize  核心线程数量

2、maximumPoolSize 线程不够用时能够创建的最大线程数

3、workQueue  任务等待队列

4、keepAliveTime 存活时间

5、threadAFactory 创建 新线程，默认的是，Executors.defaultThreadFac

会使创建的线程具有相同的优先级，并且不是守护线程

### handler：线程饱和策列

1、AbortPolicy    直接抛出异常

2、CallerRunsPolicy   用调用者所在的线程来执行任务

3、DiscardOldestPolicy   丢弃队里中最靠前的任务，并执行当前任务

4、DiscardPolicy   直接丢弃任务

5、实现RejectedExecutionHandle接口的自定义handle

### 新任务提交execute执行后的判断

1、如果运行的线程少于corePoolSize，则创建新的线程来处理任务，即使线程池中的其他线程是空闲的

2、如果线程池中的线程数量大于等于corePoolSize且小于maximumPoolSize，则只有当workQueue满时才创建新的线程去处理任务

3、如果设置的corePooSize和maximun相同，则创建的线程池的大小是固定的，这时如果有新的任务提交，若workQueue未满，则将请求放入workQueue中，等待有空闲的线程去从workQueue中取任务并处理

4、如果运行的线程数量大于等于maximumPoolSize，这时如果workQueue已经满了，则通过handle所指定的策略来处理任务

### 线程池的状态

running  能接受新提交的任务，并且也能处理阻塞队列中的任务

shutdown  不再接受新提交的任务，但可以处理存量的任务

stop  不再接受新提交的任务，也不处理存量的任务

tidying  所有任务都终止

terminated  terminated()方法执行完后进入改状态

### 线程池大小选择

1、cpu密集（主要计算）  线程数=按照核数   （核数+1）

2、IO密集  线程数量 = CPU*（1+平均等待时间/平均工作时间）



### 