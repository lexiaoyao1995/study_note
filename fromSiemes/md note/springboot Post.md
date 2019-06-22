### 关于springboot post请求

1、只获取一个json的字符串

> json
>
> {	
>
> ​	"code":"123"
>
> }

~~~java
@postmapping
public boolean isCode(@requestBody String code){
    return true;
}
~~~

2、获取json并且包装成一个类

~~~java
@postMapping
public boolean isPOJO(@requestBody Object object){
    
}
~~~

