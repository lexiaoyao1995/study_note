### Mybatis

#### 自动驼峰命名转换

springboot配置

~~~xml
mybatis.configuration.map-underscore-to-camel-case=true
~~~

数据库中字段可以对应pojo类的命名规则

user_name   -->  userName

这样可以使得resultType方便映射

resultType需要数据库的名字和字段一样才能映射（如果开启了驼峰转换，则是转换后的名字）。

resultMap则是可以自定义描述结果集Java对象的映射。

> resultMap属性
>
> > id
> >
> > type
>
> resultMap子元素
>
> > id
> >
> > result
> >
> > association
> >
> > collection

