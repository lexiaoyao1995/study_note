### ioc 和 DI DL

ioc的实现方式有DI（依赖注入）和DL（依赖查找）

spring采用的DI

### 依赖注入方式

Setter

interface

constructor

**annotation**

### ioc容器的优势

避免在各处使用new

创建实例的时候不需要了解其中的细节

### ioc生成bean的流程

1、读取bean的配置信息，填写bean的定义注册表

通过xml，或是@configuration

2、根据bean注册表实例化bean

3、将bean放到spring容器中

4、使用bean

### spring IOC支持的功能

1、**依赖注入**

2、依赖检查

3、**自动装配**

4、支持集合

5、制定初始化方法和销毁方法

6、支持回调

### springIOC容器核心接口

#### beanfactory  spring最核心的接口

1、提供ioc配置机制 

2、包含bean的各种定义，便于实例化bean

3、建立bean之间的依赖关系

4、bean的生命周期控制

##### getbean方法

1、转换beanName

2、从工厂中加载实例

3、实例化bean

4、检测parentBeanFactory

5、初始化依赖的bean

6、创建bean

#### applicationContext 继承多个接口 

1、beanfactory 能够管理，装备bean

2、resourceParrernResolver 能够加载资源文件



BeanDefinitionRegistry  向ioc容器组测接口。

DefaultListableBeanFactory 中beanDefinitionMap用于存放这些定义

~~~java
private final Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<>(256);
~~~

#### applicationContext 和 beanfactory 比较

applicationContext是面向spring开发者，功能更多

beanfactory是spring框架的基础设施，面向spring 

### refresh方法

为ioc容器以及bean的生命周期提供管理条件

刷新spring上下文，定义spring上下文加载流程

### spring bean的作用域

singleton ： spring的默认作用域，容器里唯一的bean实例

prototype：针对每个getBean请求，容器会创建一个bean实例

request：对于每个http请求，容器会创建一个bean实例

session：对于每个session，容器会创建一个bean实例

### spring的生命周期

#### 创建过程

1、实例化bean

2、aware （注入bean id 等）

3、BeanPostProcessor接口  postProcessBeforeInitialization

4、InitializingBean的方法afterPropertiesSet

5、定制bean

6、BeanPostProcessor接口  postProcessAfterInitialization

7、完毕

#### 销毁过程

DisposableBean接口destroy方法