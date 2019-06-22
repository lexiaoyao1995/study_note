### Compile Once ， Run Anywhere 如何实现

java源码首先被编译成字节码（class），再由不同平台的jvm进行解析，java语言在不同的平台运行时不需要进行重新编译，java虚拟机在执行字节码的时候，把字节码抓换成具体的机器指令。

### jvm 大致解释 架构图

jvm主要加载.class文件，主有由四个部分组成

classloader，runtime data area，execution engine 和 native interface组成

**class loader** 加载class文件到内存

**execution engine**对命令进行解析

**native interface** 融合不同开发语言的原生库为java所用

**runtime data area** （java内存模型）里包括stack，heap，method area



### 类从编译到执行的过程

1、编译器将.java源文件编译为.class字节码文件

2、classLoader将字节码转换为JVM中的Class对象

3、jvm利用Class对象实例化对象

### 谈谈ClassLoader

主要工作是在Class装载的加载阶段，主要作用是从系统外部获得Class二进制数据流，它是java的核心组件，所有的Class都是由ClassLoader进行加载的，ClassLoader负责通过Class文件里的二进制数据流装载进系统，然后交给java虚拟机进行连接，初始化。

### ClassLoader种类

1、bootstrapClassLoader ： 由c++编写  jre\lib\rt.jar

2、ExtClassLoader：java编写 加载javax.*    jre\lib\ext\*.jar

3、AppClassLoader：加载程序所在目录

4、自定义ClassLoader：java编写，定制化加载

### 双亲委派机制

自下而上，每个ClassLoader有个parent成员变量

1、自底向上检查是否加载了类是否被加载

2、自顶向下尝试加载类

### 双亲委派机制优势

避免多份同样字节码的加载

### 类的加载方式

1、隐式加载：new

2、显示加载：loadClass，forName

### LoadClass和forName的区别

#### 类的装载过载

##### 1、加载

通过classloader加载class文件字节码，生成class对象

##### 2、链接：

2.1 校验:检查安全性

2.2 准备：为类变量（static）分配存储空间，并设置类变量初始值

2.3 解析:

##### 3、初始化

类变量赋值和静态代码快

#### 区别

class.forName得到的class是已经完成初始化的

ClassLoader.loaderClass得到的class还没有链接

##### 作用

jdbc  一般用forname来完成静态代码，初始化

spring ioc  多使用classloader完成lazy load 加快效率



### java内存模型  jdk8

#### 线程的角度

线程私有：程序计数器  虚拟机栈  方法栈

线程共享：元空间metaSpace  堆

##### 程序计数器

记录所执行的字节码的行号，和线程一对一

对java方法计数，如果是对native方法计数，为undefined

不会内存泄漏

##### 栈

主要包含单个线程每个方法执行的栈帧。

栈帧用于存储局部变量表，操作数，动态链接，返回地址。

局部变量表：方法执行的所有变量

操作数栈：类似与原生CPU寄存器  入栈，出栈等

**递归为什么会引发stackoverflow** 

方法执行时会创建对应的栈帧，并压入虚拟机的栈中，每次递归会生成一个栈帧，如果递归过深会超出虚拟机栈深度。解决思路，限制递归次数。

**栈过多引发outofmenory异常**

无法申请足够多的异常     比如死循环一直创新的线程

##### 本地方法栈

与虚拟机栈类型，主要用于native方法

##### 元空间

都是用来存储class的相关信息，比如method和filed，name。

jdk1.8 元空间替代了**永久代**

元空间使用本地内存，永久代使用是jvm的内存

字符串常量池存在永久带，容易溢出，元空间没有字符串常量池，字符串常量池移动到了堆中。

metaSpace便于GC

##### java堆（heap）

对象实例的分配区域

GC管理的主要区域  可以分为新生代和老年代

### jvm三大性能调优参数 -Xms -Xmx -Xss 的含义

比如java -Xms128m -Xmx128m -Xss256k -jar xxx.jar

-Xss 规定了栈的大小

-Xms 堆的初始值

-Xmx 堆能达到的最大值

一般-Xms -Xmx 设置为一样的，因为扩容会影响程序稳定性

### java内存模型的堆和栈的区别，内存分配策略

静态存储 ：编译时确定每个数据目标在运行时的存储空间需求 

要求代码中不允许有可变数据存在，或是递归存在



栈式存储：数据区需求在编译时未知，运行时确定

堆式存储：数据区在编译时和运行时都无法确定

#### 区别

联系：引用对象时，栈中定义变量保存堆中目标的首地址

区别：

1、管理方式，栈自动释放，堆需要GC

2、空间大小，栈比较小

3、碎片相关，栈产生的碎片远小于堆

4、分配方式，栈支持静态和动态分配，堆仅仅支持动态分配

5、效率，栈的效率更高

### 字符串的intern方法jdk6和jdk6以后

jdk6 intern 将字符串放入常量池

jdk6 以后，不但将字符串放入常量池，还在堆中创建该字符串，

​		如果已经堆中已经有了，就把字符串的引用放入常量池中