### propagation  传播

propagation  required 最常用的事务，如果当前没有事务，就新建一个事务，如果已经存在一个事务中，加入到这个事务中，这是最常见的选择。

propagation  supports 支持当前事务，如果当前没有事务，就以非事务方式执行

propagation  mandatory（强制性） 必须在一个事务中运行，也就是说，只能被一个父事务调用

propagation  required new 新建事务，如果当前存在事务，把当前事务挂起

propagation  not support 以非事务的方式操作，如果当前存在事务，就把当前事务挂起

propagation  never 以非事务方式执行，如果当前存在事务，就抛出异常

propagation  nested（内嵌） 如果当前存在事务，则在嵌套事务内执行，如果当前没有事务，则执行与propagation required类似的操作，和propagation required不同的地方在于它有一个回滚点

### 关于脏读，不可重复读，虚读

脏读：在一个事务中读取到另一个事务没有提交的数据

不可重复读，在一个事务中，两次查询的结果不一样（针对update操作）

虚读（幻读），在一个事务中，两次查询的结果不一致（针对insert操作）



等级

read uncommitted

read committed

repeatable read  （mysql）

serializeable



不可重复读

（针对其他提交前后，读取**数据本身**的对比）



幻读

（针对其他提交前后，读取**数据条数**的对比）