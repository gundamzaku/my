### Spring

#### BeanFactory 和 ApplicationContext 有什么区别  
BeanFacotry是spring中比较原始的Factory。如XMLBeanFactory就是一种典型的BeanFactory。原始的BeanFactory无法支持spring的许多插件，如AOP功能、Web应用等。   
ApplicationContext 是 BeanFactory接口的子接口  
BeanFactory 采用的是延迟加载，第一次getBean的时候才会初始化Bean  
ApplicationContext是对BeanFactory的扩展，提供了更多的功能  
国际化处理  
事件传递  
Bean自动装配  
各种不同应用层的Context实现  

#### Spring Bean 的生命周期  
#### Spring IOC 如何实现  
#### 说说 Spring AOP  
#### Spring AOP 实现原理  
#### 动态代理（cglib 与 JDK）  
#### Spring 事务实现方式  
#### Spring 事务底层原理  
#### 如何自定义注解实现功能  
#### Spring MVC 运行流程  
#### Spring MVC 启动流程  
#### Spring 的单例实现原理  
#### Spring 框架中用到了哪些设计模式  
#### Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）  
