关于异常runtimeexception和exception区别

1、java将所有的错误封装成一个对象，其根本父类为throwable，throwable有两个子类，error和exception

~~~java
public class Exception extends Throwable
~~~

2、Error是throwable的子类，用于指示合理的应用程序不应该试图捕获的严重问题，大多数这样的错误都是异常条件。

3、exception类，指出了合理的应用程序想要捕获的条件。

4、runtimeexception是那些可能在java虚拟机正常运行期间抛出的异常的类，runtimeexception的任何子类都无需在exception子句中进行声明，它是exception的子类

5、异常的分类

error：一般为底层的不可恢复的错误

exception：分为 未检测异常（runtimeexception）和已检测异常（非runtimeexception）