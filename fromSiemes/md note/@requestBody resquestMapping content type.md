### 四种常见的content type

#### 1、application/x-www-form-urlencoded

主要是form提交时使用的type，键值对的形式，放在requestbody中

#### 2、multipart/form-data

上传文件必须使用这个属性

#### 3、application-json

json放在requestbody中

#### 4、text/xml

很少用到



### @requestparam和@requestbody

requestparam处理content type 为application/x-www-form-urlencoded的请求数据，包括所有的get请求和表单提交的post请求

requestbody 用来处理非application/x-www-form-urlencoded的数据请求，包括json数据传输。



总结：

1、get请求，不能使用requestbody

2、post请求，可以使用requestbody和requestparam