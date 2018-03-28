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
1、实例化一个Bean－－也就是我们常说的new；  
2、按照Spring上下文对实例化的Bean进行配置－－也就是IOC注入；  
3、如果这个Bean已经实现了BeanNameAware接口，会调用它实现的setBeanName(String)方法，此处传递的就是Spring配置文件中Bean的id值  
4、如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory(setBeanFactory(BeanFactory)传递的是Spring工厂自身（可以用这个方式来获取其它Bean，只需在Spring配置文件中配置一个普通的Bean就可以）；  
5、如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文（同样这个方式也可以实现步骤4的内容，但比4更好，因为ApplicationContext是BeanFactory的子接口，有更多的实现方法）；  
6、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessBeforeInitialization(Object obj, String s)方法，BeanPostProcessor经常被用作是Bean内容的更改，并且由于这个是在Bean初始化结束时调用那个的方法，也可以被应用于内存或缓存技术；  
7、如果Bean在Spring配置文件中配置了init-method属性会自动调用其配置的初始化方法。  
8、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法、；  
注：以上工作完成以后就可以应用这个Bean了，那这个Bean是一个Singleton的，所以一般情况下我们调用同一个id的Bean会是在内容地址相同的实例，当然在Spring配置文件中也可以配置非Singleton，这里我们不做赘述。  
9、当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用那个其实现的destroy()方法；  
10、最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。 

#### Spring IOC 如何实现  
控制反转IoC(Inversion of Control)，是一种设计思想，DI(依赖注入)是实现IoC的一种方法，也有人认为DI只是IoC的另一种说法。没有IoC的程序中我们使用面向对象编程对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为所谓控制反转就是：获得依赖对象的方式反转了。  
IoC是Spring框架的核心内容，使用多种方式完美的实现了IoC，可以使用XML配置，也可以使用注解，新版本的Spring也可以零配置实现IoC。Spring容器在初始化时先读取配置文件，根据配置文件或元数据创建与组织对象存入容器中，程序使用时再从Ioc容器中取出需要的对象。  


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
