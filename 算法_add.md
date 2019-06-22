### 数据结构考点

1、数组和链表的区别

2、链表的操作，如反转，链路环路检测，双向链表，循环链表相关操作

3、队列、栈的应用

4、二叉树的遍历方式及其递归和非递归的实现

5、红黑树的旋转



### 算法考点

1、内部排序

如 递归排序，交换排序，选择排序，插入排序

2、外部排序

应掌握如何利用有限的内存配合海量的外部存储来处理超大的数据集，写不出来也要有相关思路



那些排序是不稳定的，稳定意味着什么

不同数据集，各种排序最好或最差的情况

如何优化算法



### HashMap 

#### put方法的逻辑

1、如果HashMap未被初始化过，则初始化

2、对Key求Hash值，然后再计算下标

3、如果没有碰撞，直接放入桶中

4、如果碰撞了，以链表的方式链接到后面

5、如果链表长度超过阈值，就把链表转成红黑树

6、如果链表长度低于6，就把红黑树转回链表

7、如果节点已经存在就替换旧值

8、如果桶满了（容量16*负载因子0.75），就需要resize（扩容2倍后重排）



#### 如何有效减少碰撞

1、扰动函数：促使元素位置分布均匀，减少碰撞机会

2、使用final对象，并采用合适的equals和hashCode方法



#### 为什么hashMap的长度是2的指数倍

hash%length==hash&(length-1)的前提是length是2的n次方； 

让取模运算更高效

#### HashMap扩容的问题

1、多线程环境下，调整大小会存在条件竞争，容易造成死锁

2、rehashing是一个比较耗时的过程



### hashTable

早期java类库提供的哈希表的实现

线程安全：涉及到修改HashTable的方法，使用synchronized修饰

串行化的方式运行，性能较差

**note**

使用Collections.sychronizedMap可以将hashmap转化为线程安全的map，不过效率也很低



### 如何优化HashTable

通过锁细粒度化，将整锁拆分为多个锁进行优化

#### 早期的ConcurrentHashMap

通过分段锁segment来实现

数据结构  数组+链表



####  1.8的concurrentHashMap

使用CAS+synchronized使锁更细化

数据结构  数组+链表+红黑树

##### put方法的逻辑

1、判断node[]数组是否初始化，没有则进行初始化操作

2、通过hash定位数组的索引坐标，是否有node节点，如果没有则使用cas进行添加，添加失败则进入下一次循环

3、检测到内部正在扩容，就帮助它一块扩容

4、如果头节点不为空 f!=null，则使用synchronized锁住f元素（链表/红黑树的头元素）

5、判断链表长度是否达到8，做树化



##### 比起1.7的优化：

比起segment ，锁拆得更细

1、首先使用无锁操作cas插入头节点，失败则循环重试

2、若头节点已存在，则尝试获取头节点的同步锁，再进行操作



#### note 需要百度

1、size方法和mappingCount方法的异同，两者计算是否准确

2、多线程环境下如何扩容



#### 三者区别

1、hashMap线程不安全，数组+链表+红黑树

2、HashTable线程安全，锁住整个对象，数组+链表

3、concurrentHashMap线程安全，CAS+同步锁，数组+链表+红黑树

4、HashMap的key，value均可以为null，而其他的两个类不支持



### JUC知识点梳理

java.util.concurrent:提供并发编程的解决方法

CAS是java.util.concurrent.atomic包的基础

AQS是java.util.concurrent.locks包以及常用类比如Semophore,ReentrantLock基础

#### JUC分类

1、线程执行器executor

2、锁locks

3、原子变量类atomic

4、并发工具类tools

5、并发集合collections

#### 并发工具类

##### 1、闭锁 CountDownLatch

让主线程等待一组事件发生后继续执行

事件指的是CountDownLatch里的countDown方法

##### 2、栅栏 CyclicBarrier

阻塞当前线程，等待其他线程

等待其他线程，且会阻塞自己当前线程，所有线程必须同时达到栅栏位置后，才能继续执行

所有线程达到栅栏处，可以触发执行另外一个预先设置好的线程

##### 3、信号量 Semaphore

控制某个资源可被同时访问的线程个数

##### 4、交换器 Exchanger

两个线程到达同步点后，相互交换数据



### 阻塞队列

##### BlockingQueue：提供可阻塞的出队和入队操作

主要用于生产者消费者模式，在多线程场景时生产者线程在队列尾部添加元素，而消费者线程则在队列头部消耗元素，通过这种方式能够达到将任务的生成和消费进行隔离的目的

##### 种类

1、ArrayBlockingQueue：一个由数组结构组成的有界阻塞队列

2、LinkedBlockingQueue：一个由链表结构组成的有界/无界阻塞队列

3、PriorityBlockingQueue：一个支持优先级排序的无界阻塞队列



### java IO

#### bio：阻塞io 

#### nio：构建多路复用的，同步非阻塞的io操作

##### nio核心组成    

channels

Buffers

Selectors

##### Channels

1、fileChannel

note：

transferTo：把fileChannel中的数据拷贝到另外一个channel

transferFrom：把另外一个channel中的数据拷贝到fileChannel

避免两次用户态和内核态间的上下文切换，即零靠别，效率高

2、DatagramChannel

3、SocketChannel

4、ServerSocketChannel



#### io多路复用：调用系统级别的Select/poll/epoll

区别

1、支持一个进程能打开的最大连接数

select  上限比较小

poll  无限

epoll  上限大

2、文件剧增带来的效率问题

select  poll  线性下降

epoll  性能比较好

3、消息传递

select 和 poll 需要将消息传递到用户空间，需要内存的拷贝动作

epoll 通过内存和用户空间共享一块内存来实现，性能较高

#### AIO 异步io  基于事件和回调

##### AIO如何进一步加工处理结果

1、基于回调，实现CompletionHandle接口，调用时触发回调函数

2、返回future，通过isDone查看是否准备好，通过get等待返回数据