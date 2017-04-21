# Java基础
1. Java中创建实例化对象有哪些方式?  
①最常见的创建对象方法，使用new语句创建一个对象。  
②通过工厂方法返回对象，例:String s =String.valueOf()。（工厂方法涉及到框架）  
③动用反射机制创建实例化对象，Class类的三种方法或者通过类类型的newInstance()实例方法。  
④调用对象的clone()方法。（俗称克隆方法）  
⑤通过I/O留的反序列化手段，调用ObjectInputStream对象的readObject()方法。  

2. 接口和抽象类的区别是什么?  
Java提供和支持创建抽象类和接口。它们的实现有共同点，不同点在于：
- 接口中所有的方法隐含的都是抽象的。而抽象类则可以同时包含抽象和非抽象的方法。
- 类可以实现很多个接口，但是只能继承一个抽象类
- 类如果要实现一个接口，它必须要实现接口声明的所有方法。但是，类可以不实现抽象类声明的所有方法，当然，在这种情况下，类也必须得声明成是抽象的。
- 抽象类可以在不提供接口方法实现的情况下实现接口。
- Java接口中声明的变量默认都是final的。抽象类可以包含非final的变量。
- Java接口中的成员函数默认是public的。抽象类的成员函数可以是private，protected或者是public。
- 接口是绝对抽象的，不可以被实例化。抽象类也不可以被实例化，但是，如果它包含main方法的话是可以被调用的。

3. 进程和线程的区别是什么？创建线程有几种不同的方式？那种方式更好？
进程是执行着的应用程序，而线程是进程内部的一个执行序列。一个进程可以有多个线程。线程又叫做轻量级进程。  
有三种方式可以用来创建线程：
- 继承Thread类
- 实现Runnable接口
- 应用程序可以使用Executor框架来创建线程池
实现Runnable接口这种方式更受欢迎，因为这不需要继承Thread类。  
在应用设计中已经继承了别的对象的情况下，这需要多继承（而Java不支持多继承），只能实现接口。同时，线程池也是非常高效的，很容易实现和使用。

4. Java中的HashMap的工作原理是什么？
Java中的HashMap是以键值对(key-value)的形式存储元素的。  
HashMap需要一个hash函数，它使用hashCode()和equals()方法来向集合/从集合添加和检索元素。  
当调用put()方法的时候，HashMap会计算key的hash值，然后把键值对存储在集合中合适的索引上。  
如果key已经存在了，value会被更新成新值。HashMap的一些重要的特性是它的容量(capacity)，负载因子(load factor)和扩容极限(threshold resizing)。

5. ArrayList和LinkedList有什么区别？
ArrayList和LinkedList都实现了List接口，他们有以下的不同点：
- ArrayList是基于索引的数据接口，它的底层是数组。它可以以O(1)时间复杂度对元素进行随机访问。与此对应，
LinkedList是以元素列表的形式存储它的数据，每一个元素都和它的前一个和后一个元素链接在一起，在这种情况下，查找某个元素的时间复杂度是O(n)。
- 相对于ArrayList，LinkedList的插入，添加，删除操作速度更快，因为当元素被添加到集合任意位置的时候，不需要像数组那样重新计算大小或者是更新索引。
- LinkedList比ArrayList更占内存，因为LinkedList为每一个节点存储了两个引用，一个指向前一个元素，一个指向下一个元素。

6. 什么是orm，为什么要有ORM？ORM存在的意义？  
ORM是三个单词的缩写：Object/Relationship Mapping。翻译过来就是“对象/关系映射”。  
在用面向对象思想编写应用程序的时候，最终都是把对象的信息保存在关系型数据库中，  
这样我们就需要编写很多与底层数据库相关的SQL语句。显然这样是很不便捷的，ORM框架技术就可以解决这些繁琐的问题。  
彻底抛弃书写SQL语句的思想，完全使用面向对象的思想开发。  
为什么要抛弃程序中书写SQL语句的思想？
①不同的数据库使用的SQL语法不同，例：同样一段SQL脚本，能在T-SQL中运行，但不一定能保证可以在PL-SQL中运行。
②同样的功能在不同的数据库有不同的实现方式，例：分页SQL。
③程序过分依赖SQL，对程序的移植、扩展和维护带来很大的麻烦。  
# Spring 框架
> Spring框架Spring是一个轻量级的控制反转（IOC）和面向切面（AOP）的容器框架和开源框架。
1. 什么是Spring的AOP？
AOP：通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。
主要功能有：日志记录、性能统计、安全控制、事务处理、异常处理等。
2. 什么是Spring的MVC框架？
Spring MVC是一种前端控制器的实现形式，它的基本概念分为静态概念和动态概念。
静态概念：DispatcherServlet就是Spring MVC的前端控制器。
思路：  
①当浏览器端用户的请求通过DispatcherServlet进行了分发，到达Cotroller层。  
②到达Cotroller层之后，便生产出我们所需要的业务数据Model。  
③然后Model层再通过DispatcherServlet进行传递给我们的View层。  
④最后完成了最终的页面呈现。  
总结：MVC将业务逻辑和页面实现了分离，其核心就是通过DispatcherServlet实现的。
动态概念
①当浏览器的请求Request到达DispatcherServlet。（因为DispatcherServlet也是一个Servlet，所有的Request能够被它拦截到）  
②然后DispatcherServlet会搜索寻找到一个Mapping，也就是HandlerMaping，并将其功能代理给了HandlerMaping。  
③然后HandlerMaping根据本身的配置，找到需要用到的Controller和HandlerInterceptor。  
④然后把Controller和HandlerInterceptor制成一个可执行的链条，也就是Handler/HandlerAdapter的适配器。  
⑤Handler/HandlerAdapter的适配器将信息返回给了DispatcherServlet，DispatcherServlet便开始调用这个一般化的处理器Handler/HandlerAdapter。  
⑥Controller的目的就是生成ModelAndView模型，并且返还给DispatcherServlet。  
⑦DispatcherServlet是不会管理视图显示的，所以它就调用ViewResolver视图解析器并 通过该方法返回到View对象。（ViewResolver的作用是告诉DispatcherServlet哪个视图是用来解析当前这种场景的）  
⑧然后ModelAndView将模型数据传递到View，完成了页面呈现。    

3. Spring 框架中都用到了哪些设计模式？
Spring框架中使用到了大量的设计模式，下面列举了比较有代表性的：
- 代理模式—在AOP和remoting中被用的比较多。
- 单例模式—在spring配置文件中定义的bean默认为单例模式。
- 模板方法—用来解决代码重复的问题。比如. RestTemplate, JmsTemplate, JpaTemplate。
- 前端控制器—Spring提供了DispatcherServlet来对请求进行分发。
- 视图帮助(View Helper )—Spring提供了一系列的JSP标签，高效宏来辅助将分散的代码整合在视图里。
- 依赖注入—贯穿于BeanFactory / ApplicationContext接口的核心理念。
- 工厂模式—BeanFactory用来创建对象的实例。
