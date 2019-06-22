### 关于多表查询

example

| ID   | Name |
| ---- | ---- |
| 1    | 张三 |
| 2    | 李四 |
| 3    | 王二 |

| ID   | Cname |
| ---- | ----- |
| 1    | 足球  |
| 2    | 音乐  |
| 4    | 美术  |

#### 一、外连接

外连接分为左连接，右连接，完全外连接

##### 1、左连接 left join

~~~sql
select * from student left join course on student.ID = course.ID
~~~

> result
>
> | ID   | Name | ID   | CName |
> | ---- | ---- | ---- | ----- |
> | 1    | 张三 | 1    | 足球  |
> | 2    | 李四 | 2    | 音乐  |
> | 3    | 王二 | NULL | NULL  |

左连接包含left join左表所有行，如果右表中某行在右表中没有匹配，则结果中对应右表的部分全部为空

##### 2、右连接 right join

~~~sql
select * from student right join course on student.ID = course.ID
~~~

> result
>
> | ID   | Name | ID   | CName |
> | ---- | ---- | ---- | ----- |
> | 1    | 张三 | 1    | 足球  |
> | 2    | 李四 | 2    | 音乐  |
> | NULL | NULL | 4    | 美术  |

右连接包含right join右表所有行，如果左表中某行没有匹配，则结果集中对应左表的部分全部为空

##### 3、完全外连接full join

~~~sql
select * from student full join course on student.ID = course.ID
~~~

> result
>
> | ID   | Name | ID   | CName |
> | ---- | ---- | ---- | ----- |
> | 1    | 张三 | 1    | 足球  |
> | 2    | 李四 | 2    | 音乐  |
> | 3    | 王二 | NULL | NULL  |
> | NULL | NULL | 4    | 美术  |

#### 二、内连接

~~~sql
select * from student inner join course on student.ID = course.ID
~~~

> result
>
> | ID   | Name | ID   | CName |
> | ---- | ---- | ---- | ----- |
> | 1    | 张三 | 1    | 足球  |
> | 2    | 李四 | 2    | 音乐  |

inner join 是比较运算符，只返回符合条件的行。

#### 三、交叉连接

1、概念：没有where子句的交叉连接将产生连接所涉及的表的笛卡尔积，第一个表的行数乘以第二个表的行数等于笛卡尔结果集的大小。

~~~sql
select * from student cross join course
~~~

> result
>
> | ID   | Name | ID   | CName |
> | ---- | ---- | ---- | ----- |
> | 1    | 张三 | 1    | 足球  |
> | 2    | 李四 | 1    | 足球  |
> | 3    | 王二 | 1    | 足球  |
> | 1    | 张三 | 2    | 音乐  |
> | 2    | 李四 | 2    | 音乐  |
> | 3    | 王二 | 2    | 音乐  |
> | 1    | 张三 | 3    | 美术  |
> | 2    | 李四 | 3    | 美术  |
> | 3    | 王二 | 3    | 美术  |

**如果sql这样写就和inner join一样**

##### 我觉得比较好的写法

~~~sql
select * from student cross join course where student.ID = course.ID
~~~

### sql中ON和WHERE的区别

数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。

在使用left join时，on和where条件的区别如下：

1、on条件是在生成临时表使用的条件，它不管on中的条件是否为真，都会返回左表中的记录

2、where条件是在临时表生成好后，再对临时表进行过滤的条件，这时已经没有left join的含义了，条件不为真就全部过滤掉。





#### null

不能使用 =null 或是！=null 来查找null值。

在mysql中，null值和任何其他值的比较（即使是null）永远返回false

使用运算符 IS NULL  和 IS NOT NULL



#### alter

用于修改表的信息，包括添加，删除字段



#### 临时表

creat temporary table



#### 复制表

1、show create table 旧表   再进行粘贴

2、create table 新表 select * from 旧表 where 1=2   （仅仅是复制结构 或是）

​	create table 新表 like 旧表

3、create table 新表 select * from 旧表