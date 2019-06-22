### HashMap

hashMap是一个用存储key-value键值对的集合，每一个键值对也叫做entry，jdk1.8后叫做node，node的结构包含，hash值，key，value，以及下一个node。

这些键值对根据hash函数计算位置，分散在一个数组中，这个数组就是hashMap的主干。

如果hash函数和indexFor函数计算的位置相同，则采用链表的形式，挂在当前位置的node后面。

##### hash函数

```java
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```
这个函数其实是个扰动函数，把hash值映射得相对稀疏，不容易发生碰撞。

**indexFor**函数

计算index，index=HashCode（key）&（Length-1）；



HashMap在插入元素过多的时候需要进行resize，条件是

HashMap.size > = Capacity*loadfactor

HashMap中的resize包括扩容和rehash两个步骤，ReHash在并发的情况下可能会形成链表环，造成get操作死循环



### ConCurrentHashMap

#### 1.7

ConCurrentHashMap其实就是一个segment数组，而每一个segment又类似一个hashMap，因此ConCurrentHashMap可以说是一个二级hash表，在一个总的hash表下面，有若干个子hash表。

优势就是，采用了分段锁的技术，segment之间相互不影响。

每个segment中都有一把锁，相当于降低了锁的粒度，让并发效率更高。

get方法：

1、为输入的key做hash运算，得到hash值

2、通过hash值，定位到segment对象

3、再次通过hash值，定位到segment当中数组的具体位置。

put方法：

1、为输入的key做hash运算，得到hash值

2、通过hash值，定位到segment对象

3、获得可重入锁

4、再次通过hash值，定位到segment当中数组的具体位置。

5、插入数据

6、释放锁

##### size方法如何保证一致性

类似于乐观锁转悲观锁

先假定size过程中不会有修改，当尝试一定次数，才转为悲观锁，锁住所有segment保证一致性。

