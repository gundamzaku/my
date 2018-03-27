### 基础篇  

#### 基本功  

##### 面向对象的特征  
抽象、继承、封装、多态性  
多态性是指允许不同类的对象对同一消息作出响应。  

##### final, finally, finalize 的区别  
在Java中，final关键字可以用来修饰类、方法和变量（包括成员变量和局部变量）。  
当用final修饰一个类时，表明这个类不能被继承。  

使用final方法的原因有两个。第一个原因是把方法锁定，以防任何继承类修改它的含义；第二个原因是效率。在早期的Java实现版本中，会将final方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升。在最近的Java版本中，不需要使用final方法进行这些优化了。  

对于一个final变量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。  

##### int 和 Integer 有什么区别  
Ingeter是int的包装类，int的初值为0，Ingeter的初值为null。  
int与integer的区别从大的方面来说就是基本数据类型与其包装类的区别：  
int 是基本类型，直接存数值，而integer是对象，用一个引用指向这个对象  
int 是基本数据类型（面向过程留下的痕迹，不过是对java的有益补充），Integer 是一个类，是int的扩展，定义了很多的转换方法  
比如当需要往ArrayList，HashMap中放东西时，像int，double这种基本类型是放不进去的，因为容器都是装 object的，这是就需要这些基本类型的包装类了。  

##### 重载和重写的区别  
在Java程序中，类的继承关系可以产生一个子类，子类继承父类，它具备了父类所有的特征，继承了父类所有的方法和变量。  
子类可以定义新的特征，当子类需要修改父类的一些方法进行扩展，增大功能，程序设计者常常把这样的一种操作方法称为重写，也叫称为覆写或覆盖。  

方法重载是让类以统一的方式处理不同类型数据的一种手段。调用方法时通过传递给它们的不同个数和类型的参数来决定具体使用哪个方法，这就是多态性。  
所谓方法重载是指在一个类中，多个方法的方法名相同，但是参数列表不同。参数列表不同指的是参数个数、参数类型或者参数的顺序不同。  

##### 抽象类和接口有什么区别  
1、在抽象类中可以写非抽象的方法，从而避免在子类中重复书写他们，这样可以提高代码的复用性，这是抽象类的优势；接口中只能有抽象的方法。
2、一个类只能继承一个直接父类，这个父类可以是具体的类也可是抽象类；但是一个类可以实现多个接口。

##### 说说反射的用途及实现  
允许运行中的 Java 程序获取自身的信息，并且可以操作类和对象的内部属性。  

通过反射，我们可以在运行时获得程序或程序集中每一个类型成员和成员变量的信息。  

当我们在使用 IDE（如 Eclipse\IDEA）时，当我们输入一个队长或者类并向调用它的属性和方法时，一按 (“.”)点号，编译器就会自动列出她的属性或方法，这里就会用到反射  

很多框架（比如 Spring）都是配置化的（比如通过 XML文件配置 JavaBean，Action之类的），为了保证框架的通用性，他们可能根据配置文件加载不同的对象或类，调用不同的方法，这个时候就必须用到反射——运行时动态加载需要加载的对象。  

##### 说说自定义注解的场景及实现  
Annotation(注解)是JDK5.0及以后版本引入的。它可以用于创建文档，跟踪代码中的依赖性，甚至执行基本编译时检查。  

解是以‘@注解名’在代码中存在的，根据注解参数的个数，我们可以将注解分为：标记注解、单值注解、完整注解三类。它们都不会直接影响到程序的语义，只是作为注解（标识）存在，我们可以通过反射机制编程实现对这些元数据（用来描述数据的数据）的访问。  
在日常編程中，我們遇到的註解有@Override、@SuppressWarnings等等，@Override表示重寫父類的方法，@SuppressWarnings表示忽略警告信息。  

##### HTTP 请求的 GET 与 POST 方式的区别  
操……略  

#### session 与 cookie 区别  
操……略  

##### session 分布式处理  
1.基于数据库的Session共享  
2.基于NFS共享文件系统  
3.基于memcached 的session  
4.基于resin/tomcat web容器本身的session复制机制  
5.基于TT/Redis 或 jbosscache 进行 session 共享。  
6.基于cookie 进行session共享  

##### JDBC 流程  
注册驱动、连接数据库、创建搬运工statement、搬运数据,执行SQL语句、处理结果集、关闭连接  

##### MVC 设计思想  
M他妈的VC，现在都前后端分离了，后端只提供API  

##### equals 与 == 的区别  
== 比较的是变量(栈)内存中存放的对象的(堆)内存地址，用来判断两个对象的地址是否相同，即是否是指相同一个对象。比较的是真正意义上的指针操作。  
equals用来比较的是两个对象的内容是否相等，由于所有的类都是继承自java.lang.Object类的，所以适用于所有对象，如果没有对该方法进行覆盖的话，调用的仍然是Object类中的方法，而Object中的equals方法返回的却是==的判断。  
```java
public boolean equals(Object obj) {
    return (this == obj);
}
```
Object.class给出equals()方法的定义，竟然只是简单地通过==去实现判断。而==在java中用于判断存储在栈中的值是否相等。我们的基本数据类型像int的比较都用==，因为基本数据类型就存放在栈中，同样存放在栈中的，还有引用数据类型的引用，而真正的对象本身则存放在堆中。因此，这里给出的equals()方法就只是比较两个对象在内存中的引用（即地址）是否相等。本例中新建了两个对象，在内存中就新开辟了两个内存空间，引用地址当然是不一样的，程序运行结果当然是不相同。  

#### 集合

##### List 和 Set 区别  
list和set是实现了collection接口的。
List：
1.可以允许重复的对象。
2.可以插入多个null元素。
3.是一个有序容器，保持了每个元素的插入顺序，输出的顺序就是插入的顺序。
4.常用的实现类有 ArrayList、LinkedList 和 Vector。ArrayList 最为流行，它提供了使用索引的随意访问，而 LinkedList 则对于经常需要从 List 中添加或删除元素的场合更为合适。

Set：
1.不允许重复对象  
2. 无序容器，你无法保证每个元素的存储顺序，TreeSet通过 Comparator  或者 Comparable 维护了一个排序顺序。  
3. 只允许一个 null 元素  
4.Set 接口最流行的几个实现类是 HashSet、LinkedHashSet 以及 TreeSet。最流行的是基于 HashMap 实现的 HashSet；TreeSet 还实现了 SortedSet 接口，因此 TreeSet 是一个根据其 compare() 和 compareTo() 的定义进行排序的有序容器。  

##### List 和 Map 区别  

1.Map不是collection的子接口或者实现类。Map是一个接口。  
2.Map 的 每个 Entry 都持有两个对象，也就是一个键一个值，Map 可能会持有相同的值对象但键对象必须是唯一的。  
3.TreeMap 也通过 Comparator  或者 Comparable 维护了一个排序顺序。  
4.Map 里你可以拥有随意个 null 值但最多只能有一个 null 键。  
5.Map 接口最流行的几个实现类是 HashMap、LinkedHashMap、Hashtable 和 TreeMap。（HashMap、TreeMap最常用）  

##### Arraylist 与 LinkedList 区别  

如果你经常会使用索引来对容器中的元素进行访问，那么 List 是你的正确的选择。如果你已经知道索引了的话，那么 List 的实现类比如 ArrayList 可以提供更快速的访问,如果经常添加删除元素的，那么肯定要选择LinkedList。  

如果你想容器中的元素能够按照它们插入的次序进行有序存储，那么还是 List，因为 List 是一个有序容器，它按照插入顺序进行存储。  

如果你想保证插入元素的唯一性，也就是你不想有重复值的出现，那么可以选择一个 Set 的实现类，比如 HashSet、LinkedHashSet 或者 TreeSet。所有 Set 的实现类都遵循了统一约束比如唯一性，而且还提供了额外的特性比如 TreeSet 还是一个 SortedSet，所有存储于 TreeSet 中的元素可以使用 Java 里的 Comparator 或者 Comparable 进行排序。LinkedHashSet 也按照元素的插入顺序对它们进行存储。  

如果你以键和值的形式进行数据存储那么 Map 是你正确的选择。你可以根据你的后续需要从 Hashtable、HashMap、TreeMap 中进行选择。  

HashSet较HashMap来说比较慢

##### ArrayList 与 Vector 区别  

Vector的方法都是同步的(Synchronized),是线程安全的(thread-safe)，而ArrayList的方法不是，由于线程的同步必然要影响性能，因此,ArrayList的性能比Vector好。  

当Vector或ArrayList中的元素超过它的初始大小时,Vector会将它的容量翻倍,而ArrayList只增加50%的大小，这样,ArrayList就有利于节约内存空间。  

##### HashMap 和 Hashtable 的区别  

HashMap和Hashtable都实现了Map接口，但决定用哪一个之前先要弄清楚它们之间的分别。主要的区别有：线程安全性，同步(synchronization)，以及速度。  

HashMap几乎可以等价于Hashtable，除了HashMap是非synchronized的，并可以接受null(HashMap可以接受为null的键值(key)和值(value)，而Hashtable则不行)。

HashMap是非synchronized，而Hashtable是synchronized，这意味着Hashtable是线程安全的，多个线程可以共享一个Hashtable；而如果没有正确的同步的话，多个线程是不能共享HashMap的。Java 5提供了ConcurrentHashMap，它是HashTable的替代，比HashTable的扩展性更好。  

另一个区别是HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛出ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。但这并不是一个一定发生的行为，要看JVM。这条同样也是Enumeration和Iterator的区别。  

由于Hashtable是线程安全的也是synchronized，所以在单线程环境下它比HashMap要慢。如果你不需要同步，只需要单一线程，那么使用HashMap性能要好过Hashtable。  

HashMap不能保证随着时间的推移Map中的元素次序是不变的。

##### HashSet 和 HashMap 区别  

HashSet实现了Set接口，它不允许集合中有重复的值，当我们提到HashSet时，第一件事情就是在将对象存储在HashSet之前，要先确保对象重写equals()和hashCode()方法，这样才能比较对象的值是否相等，以确保set中没有储存相等的对象。如果我们没有重写这两个方法，将会使用这个方法的默认实现。  

HashMap实现了Map接口，Map接口对键值对进行映射。Map中不允许重复的键。Map接口有两个基本的实现，HashMap和TreeMap。TreeMap保存了对象的排列次序，而HashMap则不能。HashMap允许键和值为null。HashMap是非synchronized的，但collection框架提供方法能保证HashMap synchronized，这样多个线程同时访问HashMap时，能保证只有一个线程更改Map。  

##### HashMap 和 ConcurrentHashMap 的区别  

从ConcurrentHashMap代码中可以看出，它引入了一个“分段锁”的概念，具体可以理解为把一个大的Map拆分成N个小的HashTable，根据key.hashCode()来决定把key放到哪个HashTable中。  

ConcurrentHashMap的工作机制，通过把整个Map分为N个Segment（类似HashTable），可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。

##### HashMap 的工作原理及代码实现  

通过hash的方法，通过put和get存储和获取对象。存储对象时，我们将K/V传给put方法时，它调用hashCode计算hash从而得到bucket位置，进一步存储，HashMap会根据当前bucket的占用情况自动调整容量(超过Load Facotr则resize为原来的2倍)。获取对象时，我们将K传给get，它调用hashCode计算hash从而得到bucket位置，并进一步调用equals()方法确定键值对。如果发生碰撞的时候，Hashmap通过链表将产生碰撞冲突的元素组织起来，在Java 8中，如果一个bucket中碰撞冲突的元素超过某个限制(默认是8)，则使用红黑树来替换链表，从而提高速度。  


##### ConcurrentHashMap 的工作原理及代码实现  

HashTable容器在竞争激烈的并发环境下表现出效率低下的原因，是因为所有访问HashTable的线程都必须竞争同一把锁。那假如容器里有多把锁，每一把锁用于锁容器其中一部分数据，那么当多线程访问容器里不同数据段的数据时，线程间就不会存在锁竞争，从而可以有效的提高并发访问效率，这就是ConcurrentHashMap所使用的锁分段技术，首先将数据分成一段一段的存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据的时候，其他段的数据也能被其他线程访问。另外，ConcurrentHashMap可以做到读取数据不加锁，并且其内部的结构可以让其在进行写操作的时候能够将锁的粒度保持地尽量地小，不用对整个ConcurrentHashMap加锁。

ConcurrentHashMap是由Segment数组结构和HashEntry数组结构组成。Segment是一种可重入锁ReentrantLock，在ConcurrentHashMap里扮演锁的角色，HashEntry则用于存储键值对数据。一个ConcurrentHashMap里包含一个Segment数组，Segment的结构和HashMap类似，是一种数组和链表结构，一个Segment里包含一个HashEntry数组，每个HashEntry是一个链表结构的元素， 每个Segment守护着一个HashEntry数组里的元素，当对HashEntry数组的数据进行修改时，必须首先获得它对应的Segment锁。  


