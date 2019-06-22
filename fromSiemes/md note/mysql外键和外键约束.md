### mysql 关于外键和外键约束

#### 外键 是一个逻辑上东西

几个概念：

person表里有一个classid，则是外键

class表的主键id，是主键

person以公共关键字作为外键，所以是从表，外表

class以公共关键字作为主键，所以是父表，主表

#### 外键约束是真实存在的东西

有

on delete：

1、cascade：删除主键表的同事，外键表的关联行同时删除

2、no action 、 restrict（默认）：当主键表中删除对应的记录时，首先检查记录是否有对应外键，如果有则不允许删除

3、set null

在主表删除记录时，首先检查记录是否有对应外键，如果有则设置字表中有该外键值为null

### 事务开启

~~~mysql
START TRANSACTION;
INSERT INTO test1 VALUES(NULL , 200);
INSERT INTO test2 VALUES(NULL , 'asd');#error
COMMIT;
~~~

#### 坑

是······ 不是单引号‘’

~~~sql
USE demo;
CREATE TABLE `test`(
	`id` INT PRIMARY KEY,
	`name` VARCHAR(200)
);
~~~

where子句是不区分大小写的，可以使用binary关键字来设定where子句的字符串比较是区分大小写的。



#### like

子句中使用%来表示任意符号，符号_匹配一个字符

如果没有使用百分号%，like子句与等号=的效果是一样的

>%a 以a结尾的数据
>
>a% 以a开头的数据
>
>%a% 含有a的数据 
>
> _ a _  三位且中间字母a的
>
>_ a  两位且结尾字母a
>
>a _  两个且开头字母a



#### union

用于连接两个以上的select语句的结果组合合到一个结果集合中



#### order by

asc升序默认

desc降序

注意 拼音排序

如果字符集是gbk（汉字编码字符集），直接在后面加order by



如果是utf8，需要先对字段进行转码然后排序

select * from tb order by CONVERT（name using gbk）

#### Group by

根据一个或多个列，对结果进行分组

1、group by 可以实现一个简单的去重查询，假设想看下有哪些员工。除了用distinct，还可以用

select name from employee group by name



