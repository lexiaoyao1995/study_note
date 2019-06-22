## exception和error的区别

### 从概念角度解析java异常机制

1、error：程序无法处理的系统错误，编译器不做检查

2、Exception：程序可以处理的异常

3、总结：前者是程序无法处理的错误，后者是可以处理的异常



**Throwable**下有Error和Exception

**RuntimeException和非RuntimeException**



### 常见的Error和Exception

#### RuntimeException

NullPointException

ClassCastException

IllegalArgumentException 传递非法参数异常

IndexOutOfBoundsException 下标越界异常

NumberFormatException



#### 非RuntimeException

1、ClassNotFoundException    Class.forname一般会用到

2、IOException



#### Error

1、NoClassDefFoundError   

类依赖的class或者jar不存在

类文件存在，但是存在不同域中

2、StackOverFlowError

3、OutOfMemoryError



### Java异常处理消耗性能的地方

1、try-catch块影响jvm的优化

2、异常对象实例需要保存栈快照等信息，开销较大