### GC 触发时间

我的回答：

gc主要是对堆内存进行回收，虚拟机堆又分为新生代和老年代，针对新生代主要是minor GC，其触发时间是新生代中的eden区满时，针对于老年代主要是full GC，它的触发时机是老年代空间不足，或是系统调用System.gc，但这个方法只是建议执行，并不会一定执行。

### GC的对象

我的回答：

gc的对象是被标记成垃圾的对象，主要有两个方式来确定一个对象是否需要被回收，第一种是引用计数法，第二种是可达性分析，即是一个对象没有和任何引用链相连，并且在第一次标记后，在finalize方法里没有把它添加进引用链。

### GC做了什么

主要是将对象的内存释放掉，但实现方式有很多种，在新生代主要用的算法是复制算法，年轻代常用的垃圾回收器有serial收集器，ParNew收集器，parallel Scanvage 收集器，老年代主要用的算法是标记清除算法，或是标记整理算法，主要的垃圾回收器有serial old收集器，parallel收集器，CMS收集器





### 谈谈CMS收集器

cms收集器是基于标记清除算法实现的，主要有四个步骤

1、初始标记

标记GC root能直接关联的对象，需要stop the world

2、并发标记

标记全部对象 GC roots tracing

3、重新标记

修正并发标记期间，因用户程序继续运作而导致标记变动的那一步分对象的标记部分

4、并发清除

优点：并发收集，低停顿

缺点：内存碎片化



### G1收集器

garbage first：优势

1、利用算法是标记整理算法，所以不会造成内存碎片化，分配大对象时候不会因为无法找到连续的空间而提前出发GC

2、可预测停顿