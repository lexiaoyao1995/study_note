## 一级缓存

### 一级缓存介绍

在应用运行过程中，我们有可能在一次数据库会话中，执行多次查询条件完全相同的SQL，MyBatis提供了一级缓存的方案优化这部分场景，如果是相同的SQL语句，会优先命中一级缓存，避免直接对数据库进行查询，提高性能。具体执行过程如下图所示。

每个SqlSession中持有了Executor，每个Executor中有一个LocalCache。当用户发起查询时，MyBatis根据当前执行的语句生成`MappedStatement`，在Local Cache进行查询，如果缓存命中的话，直接返回结果给用户，如果缓存没有命中的话，查询数据库，结果写入`Local Cache`，最后返回结果给用户。具体实现类的类关系图如下图所示。 

我们来看看如何使用MyBatis一级缓存。开发者只需在MyBatis的配置文件中，添加如下语句，就可以使用一级缓存。共有两个选项，`SESSION`或者`STATEMENT`，默认是`SESSION`级别，即在一个MyBatis会话中执行的所有语句，都会共享这一个缓存。一种是`STATEMENT`级别，可以理解为缓存只对当前执行的这一个`Statement`有效。 

<setting name="localCacheScope" value="SESSION"/> 

### 总结

1. MyBatis一级缓存的生命周期和SqlSession一致。
2. MyBatis一级缓存内部设计简单，只是一个没有容量限定的HashMap，在缓存的功能性上有所欠缺。
3. MyBatis的一级缓存最大范围是SqlSession内部，有多个SqlSession或者分布式的环境下，数据库写操作会引起脏数据，建议设定缓存级别为Statement。

## 二级缓存

### 二级缓存介绍

在上文中提到的一级缓存中，其最大的共享范围就是一个SqlSession内部，如果多个SqlSession之间需要共享缓存，则需要使用到二级缓存。开启二级缓存后，会使用CachingExecutor装饰Executor，进入一级缓存的查询流程前，先在CachingExecutor进行二级缓存的查询，具体的工作流程如下所示。

二级缓存开启后，同一个namespace下的所有操作语句，都影响着同一个Cache，即二级缓存被多个SqlSession共享，是一个全局的变量。

当开启缓存后，数据的查询执行的流程就是 二级缓存 -> 一级缓存 -> 数据库。

 二级缓存配置

要正确的使用二级缓存，需完成如下配置的。

1. 在MyBatis的配置文件中开启二级缓存。

```
<setting name="cacheEnabled" value="true"/>
```

### 总结

1. MyBatis的二级缓存相对于一级缓存来说，实现了`SqlSession`之间缓存数据的共享，同时粒度更加的细，能够到`namespace`级别，通过Cache接口实现类不同的组合，对Cache的可控性也更强。
2. MyBatis在多表查询时，极大可能会出现脏数据，有设计上的缺陷，安全使用二级缓存的条件比较苛刻。
3. 在分布式环境下，由于默认的MyBatis Cache实现都是基于本地的，分布式环境下必然会出现读取到脏数据，需要使用集中式缓存将MyBatis的Cache接口实现，有一定的开发成本，直接使用Redis、Memcached等分布式缓存可能成本更低，安全性也更高。



spring 事务

required

requires_new

mandatory

never

not_support 

supports



1 事务的传播属性（Propagation） 

1) REQUIRED ，这个是默认的属性  required
Support a current transaction, create a new one if none exists. 
如果存在一个事务，则支持当前事务。如果没有事务则开启一个新的事务。 
被设置成这个级别时，会为每一个被调用的方法创建一个逻辑事务域。如果前面的方法已经创建了事务，那么后面的方法支持当前的事务，如果当前没有事务会重新建立事务。 
如图所示： 

2) MANDATORY  mandatory
Support a current transaction, throw an exception if none exists.支持当前事务，如果当前没有事务，就抛出异常。 

3) NEVER  never
Execute non-transactionally, throw an exception if a transaction exists. 
以非事务方式执行，如果当前存在事务，则抛出异常。 

4) NOT_SUPPORTED   not_support 
Execute non-transactionally, suspnd the current transaction if one exists. 
以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。 

5) REQUIRES_NEW  requires_new
Create a new transaction, suspend the current transaction if one exists. 
新建事务，如果当前存在事务，把当前事务挂起。 
如图所示： 

6) SUPPORTS  supports
Support a current transaction, execute non-transactionally if none exists. 
支持当前事务，如果当前没有事务，就以非事务方式执行。 

7) NESTED 
Execute within a nested transaction if a current transaction exists, behave like PROPAGATION_REQUIRED else. 
支持当前事务，新增Savepoint点，与当前事务同步提交或回滚。 
嵌套事务一个非常重要的概念就是内层事务依赖于外层事务。外层事务失败时，会回滚内层事务所做的动作。而内层事务操作失败并不会引起外层事务的回滚。 

8) PROPAGATION_NESTED 与PROPAGATION_REQUIRES_NEW的区别 

--------------------- 
作者：吃瓜群众-江郎才尽 
来源：CSDN 
原文：https://blog.csdn.net/weixin_36666151/article/details/78129413 
版权声明：本文为博主原创文章，转载请附上博文链接！