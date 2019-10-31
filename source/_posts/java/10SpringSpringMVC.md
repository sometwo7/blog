---
title: Spring/Spring MVC
date: 2019-10-04 19:49:20
tags: [Java,Spring]
categories: [Java学习]
comments: true
---
# Spring/Spring MVC

## 为什么要使用 spring？

- 简介
 - 目的：解决企业应用开发的复杂性
 - 功能：使用基本的JavaBean代替EJB，并提供了更多的企业应用功能
 - 范围：任何Java应用
 - 简单来说，Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器框架。

- 轻量　　
 - 从大小与开销两方面而言Spring都是轻量的。
 - 完整的Spring框架可以在一个大小只有1MB多的JAR文件里发布。
 - 并且Spring所需的处理开销也是微不足道的。
 - 此外，Spring是非侵入式的：典型地，Spring应用中的对象不依赖于Spring的特定类。

- 控制反转　　
 - Sping通过一种称作控制反转（IoC）的技术促进了松耦合。
 - 当应用了IoC，一个对象依赖的其它对象会通过被动的方式传递进来，而不是这个对象自己创建或者查找依赖对象。
 - 你可以认为IoC与JNDI相反——不是对象从容器中查找依赖，而是容器在对象初始化时不等对象请求就主动将依赖传递给它。

- 面向切面　　
 - Spring提供了面向切面编程的丰富支持，
 - 允许通过分离应用的业务逻辑与系统级服务（例如审计（auditing）和事务（transaction）管理）进行内聚性的开发。
 - 应用对象只实现它们应该做的——完成业务逻辑——仅此而已。
 - 它们并不负责（甚至是意识）其它的系统级关注点，例如日志或事务支持。

- 容器
 - Spring包含并管理应用对象的配置和生命周期，在这个意义上它是一种容器，
 - 你可以配置你的每个bean如何被创建——基于一个可配置原型（prototype），
 - 你的bean可以创建一个单独的实例或者每次需要时都生成一个新的实例——以及它们是如何相互关联的。
 - 然而，Spring不应该被混同于传统的重量级的EJB容器，它们经常是庞大与笨重的，难以使用。

- 框架
 - Spring可以将简单的组件配置、组合成为复杂的应用。
 - 在Spring中，应用对象被声明式地组合，典型地是在一个XML文件里。
 - Spring也提供了很多基础功能（事务管理、持久化框架集成等等），将应用逻辑的开发留给了你。

- 所有Spring的这些特征使你能够编写更干净、更可管理、并且更易于测试的代码。它们也为Spring中的各种模块提供了基础支持。

## Spring的设计模式有几种？

- 9种。

- 简单工厂：FactoryBean。
- 工厂方法：xml文件的factory-bean属性指定工厂方法。
- 单例模式：默认唯一的访问点是BeanFactory访问点。
- 适配器模式：HanderAdapter，AdvisorAdaptor。
- 装饰器模式：Wrapper，Decorator。
- 代理模式：AOP功能的原理就使用代理模式。
- 观察者模式：监听器。
- 策略模式：实例化对象的时候使用策略模式。
- 模板方法模式：JdbcTemplate。


## spring 有哪些主要模块？

- 主要有七个模块；

- 核心容器（Spring Core）
 - 核心容器提供Spring框架的基本功能。
 - Spring以bean的方式组织和管理Java应用中的各个组件及其关系。
 - Spring使用BeanFactory来产生和管理Bean，它是工厂模式的实现。
 - BeanFactory使用控制反转(IoC)模式将应用的配置和依赖性规范与实际的应用程序代码分开。

- 应用上下文（Spring Context）
 - Spring上下文是一个配置文件，向Spring框架提供上下文信息。
 - Spring上下文包括企业服务，如JNDI、EJB、电子邮件、国际化、校验和调度功能。

- Spring面向切面编程（Spring AOP）
 - 通过配置管理特性，Spring AOP 模块直接将面向方面的编程功能集成到了 Spring框架中。
 - 所以，可以很容易地使 Spring框架管理的任何对象支持 AOP。
 - Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。
 - 通过使用 Spring AOP，不用依赖 EJB 组件，就可以将声明性事务管理集成到应用程序中。

- JDBC和DAO模块（Spring DAO）
 - JDBC、DAO的抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理，和不同数据库供应商所抛出的错误信息。
 - 异常层次结构简化了错误处理，并且极大的降低了需要编写的代码数量，比如打开和关闭链接。

- 对象实体映射（Spring ORM）
 - Spring框架插入了若干个ORM框架，从而提供了ORM对象的关系工具，
 - 其中包括了Hibernate、JDO和 IBatis SQL Map等，所有这些都遵从Spring的通用事物和DAO异常层次结构。

- Web模块（Spring Web）
 - Web上下文模块建立在应用程序上下文模块之上，为基于web的应用程序提供了上下文。
 - 所以Spring框架支持与Struts集成，web模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。

- MVC模块（Spring Web MVC）
 - MVC框架是一个全功能的构建Web应用程序的MVC实现。
 - 通过策略接口，MVC框架变成为高度可配置的。
 - MVC容纳了大量视图技术，其中包括JSP、POI等，
 - 模型来有JavaBean来构成，存放于 model 当中，而视图是一个接口，负责实现模型，控制器表示逻辑代码，由c的事情。
 - Spring框架的功能可以用在任何J2EE服务器当中，大多数功能也适用于不受管理的环境。
 - Spring的核心要点就是支持不绑定到特定J2EE服务的可重用业务和数据的访问的对象，
 - 毫无疑问这样的对象可以在不同的J2EE环境，独立应用程序和测试环境之间重用。

## Spring容器有几种？

- BeanFactory是最简答的容器，提供了基本的DI支持。最常用的BeanFactory实现就是XmlBeanFactory类。
- ApplicationContext扩展了BeanFactory的功能，提供面向应用的服务。
- 通过缓存在map中，实现了类的复用。

## beanfactory和applicationcontext是什么关系，使用有什么区别。

- ApplicationContex提供了一种解析文本消息的方法，一种加载文件资源（如图像）的通用方法，它们可以将事件发布到注册为侦听器的bean。
- 此外，可以在应用程序上下文中以声明方式处理容器中的容器或容器上的操作，这些操作必须以编程方式与Bean Factory一起处理。
- ApplicationContex实现MessageSource，一个用于获取本地化消息的接口，实际的实现是可插入的。

## FactoryBean如何使用？

- 一般情况下，Spring通过反射机制利用bean的class属性指定实现类来实例化bean. 
- 如果类的配置复杂，那么就可以实现一个FactoryBean接口的工厂类，在getObject()方法中定制实例化逻辑。
- 当使用这个类的时候，Spring通过反射机制发现这个类实现了该工厂接口，就通过getObject()方法返回实例。
- 如果要获得工厂类本身的实例，则需要在beanName前面加"&"。


# AOP和IOC

## 解释一下什么是 aop？

- 面向方面的编程（AOP）是一种编程技术，它允许程序员模块化横切关注点或行为，这些问题或行为跨越典型的责任分工，例如日志记录和事务管理。

- AOP（Aspect-Oriented Programming，面向方面编程），可以说是OOP（Object-Oriented Programing，面向对象编程）的补充和完善。

- OOP（Object-Oriented Programing，面向对象编程）
 - OOP引入封装、继承和多态性等概念来建立一种对象层次结构，用以模拟公共行为的一个集合。
 - 当我们需要为分散的对象引入公共行为的时候，OOP则显得无能为力。
 - 也就是说，OOP允许你定义从上到下的关系，但并不适合定义从左到右的关系。
 - 例如日志功能。日志代码往往水平地散布在所有对象层次中，而与它所散布到的对象的核心功能毫无关系。
 - 对于其他类型的代码，如安全性、异常处理和透明的持续性也是如此。
 - 这种散布在各处的无关的代码被称为横切（cross-cutting）代码，在OOP设计中，它导致了大量代码的重复，而不利于各个模块的重用。

- AOP（Aspect-Oriented Programming，面向方面编程）
 - 它利用一种称为“横切”的技术，剖解开封装的对象内部，
 - 并将那些影响了多个类的公共行为封装到一个可重用模块，并将其名为“Aspect”，即方面。
 - 所谓“方面”，简单地说，就是将那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，
 - 便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可操作性和可维护性。
 - AOP代表的是一个横向的关系，如果说“对象”是一个空心的圆柱体，其中封装的是对象的属性和行为；
 - 那么面向方面编程的方法，就仿佛一把利刃，将这些空心圆柱体剖开，以获得其内部的消息。而剖开的切面，也就是所谓的“方面”了。
 - 然后它又以巧夺天功的妙手将这些剖开的切面复原，不留痕迹。

- 使用“横切”技术，AOP把软件系统分为两个部分：核心关注点和横切关注点。
 - 业务处理的主要流程是核心关注点，与之关系不大的部分是横切关注点。
 - 横切关注点的一个特点是，他们经常发生在核心关注点的多处，而各处都基本相似。
 - 比如权限认证、日志、事务处理。
 - AOP 的作用在于分离系统中的各种关注点，将核心关注点和横切关注点分离开来。
 - AOP的核心思想就是，将应用程序中的商业逻辑同对其提供支持的通用服务进行分离。

## Spring AOP中的关注点和交叉关注点之间有什么区别？

- 关注点是我们希望在应用程序模块中拥有的行为。关注点可以定义为我们想要实现的功能。

- 跨领域的关注点是一个适用于整个应用程序的问题，它会影响整个应用程序。例如，日志记录，安全性和数据传输是应用程序几乎每个模块都需要的问题，因此它们是跨领域的问题。

## 解释一下什么是 ioc？

- IOC是Inversion of Control的缩写，多数书籍翻译成“控制反转”。
- 把复杂系统分解成相互合作的对象，这些对象类通过封装以后，内部实现对外部是透明的，从而降低了解决问题的复杂度，而且可以灵活地被重用和扩展。

## AOP和IOC的原理是什么？

- ioc控制反转是由Spring容器负责创建对象，管理对象（DI），装配对象，配置对象，并且管理这些对象的整个生命周期。

- di依赖注入是spring容器根据描述配置将被依赖的类通过构造器或者setter方法注入正在被实例化的类。

- aop切面编程是通过抽取公共的日志、权限、事务等切面逻辑，通过jdk或者cglib的动态代理生成代理类将增强代码织入原代码中。合并类的公共处理逻辑可以减少重复代码和耦合，侵入性小，便于容器测试。

- AOP 和 IOC是Spring精华部分，AOP可以看做是对OOP的补充，对代码进行横向的扩展，通过代理模式实现，代理模式有静态代理，动态代理，Spring利用的是动态代理，在程序运行过程中将增强代码织入原代码中。

## spring 常用的注入方式有哪些？

- set 注入
- 构造方法注入
- 接口注入

## 如何创建动态AOP代理？

- 创建代理的步骤：获取增强方法/增强器，根据增强方法/增强器进行代理。

- 目标对象如果实现了接口，默认通过JDK代理，也可以强制cglib代理。如果没有实现接口，就必须使用cglib库，Spring会自动实现jdk动态代理和cglib之间的转换。

- 加载时织入(LTW)是在虚拟机载入字节码文件是动态植入AspectJ切面。LTM参数在虚拟机层面的的设置不够具体，Spring的对LTW的设置可以在类加载器的粒度上打开，通过外部增强实现效果，就不必在工程内部修改代码。

## 如何创建静态AOP代理？
- 将动态代理改为静态代理，配置文件需要添加：`<context:load-time-weaver />`，然后在META-INF文件夹下建立aop.xml：

```
<!DOCTYPE aspectj PUBLIC "-//AspectJ//DTD//EN" "http://www.eclipse.org/aspectj/dtd/aspectj.dtd">
<aspectj>
	<weaver><include within="xx.*" /></weaver>
	<aspects><aspect name="xx.AspectConfig" /></aspects>
</aspectj>
```

# Spring Bean

## Spring bean的定义和作用域是什么？

- Spring Beans是构成Spring应用程序主干的Java对象。
 - 它们由Spring IoC容器实例化，组装和管理。
 - 这些bean是使用提供给容器的配置元数据创建的，例如，以XML定义的形式。

- bean的作用域包括单例，原型，请求，回话，全局。

## Bean的生命周期是什么？

- 创建Bean的实例；
- 按照配置注入属性；
- 调用可能实现的BeanNameAware接口方法，传参id。
- 调用可能实现的BeanFactoryAware接口方法，传参Spring工厂。
- 调用可能实现的ApplicationContextAware接口方法，传参Spring上下文。
- 调用可能关联的BeanPostProcessor接口的初始化前方法。
- 调用可能配置的init-method初始化方法。
- 调用可能关联的BeanPostProcessor接口的初始化后方法。开始使用。
- 销毁时，调用可能实现的DisposableBean的destroy方法。
- 最后，调用可能配置的destroy-method销毁方法。

## bean的加载过程是什么？

- 转换对应的beanName。
- 尝试从缓存中加载单例。
- bean的实例化。
- 对原型模式检查类的依赖。
- 检查父类工厂。
- 转化bean的定义类。
- 寻找依赖。
- 针对不同的scope创建bean。
- 类型转换。

## Spring中如何让A和B两个bean按顺序加载？

- 用dependon注解依赖关系。

## 什么是循环依赖，Spring如何解决？

- 循环依赖就是循环引用，方法之间的环调用，构成有向环。 
 - Spring的构造器循环依赖将正在创建的 beanName(id) 标志符记录到“当前创建bean池”（构造状态表），
 - 构造所需的类的beanName继续添加到表中，如果已有记录，就说明有环结构，抛出循环依赖的异常。

- Spring的setter注入的循环依赖是通过提前暴露刚构造完（尚未setter注入）的bean来完成的，且只能解决单例范围的依赖。
 - 通过提前暴露一个单例工厂方法，使其他bean能引用到该bean，把beanName标志符加入到“当前创建bean池”中，
 - 然后setter注入后续类，后续类因此创建单例，加入自己的标志符。
 - 当后续类检测到setter需要的类已经位于池中，就通过该标志符在另一个表中找到对应的ObjectFactory工厂，
 - 进而返回工厂类创建的bean. 然后在第二个循环中依次setter注入工厂类创建的bean。

- Spring的prototype作用域的bean, Spring容器无法完成依赖注入，因为不缓存该作用域的bean,因此无法提前暴露。

## 如何获取单例？

- 在全局变量加锁的情况下。
- 检查singletonObjects缓存类中是否已加载，
- 没有加载就把beanName记录到加载状态表，
- 通过ObjectFactory的方法得到实例化bean，
- 从加载状态表中移除这个beanName，
- 缓存实例并删除其他状态表的记录。

## 如何从缓存中获取单例bean？

- 创建单例的时候会存在依赖注入的情况，
- 而在创建依赖的时候为了避免循环依赖，
- Spring创建Bean的原则是不等bean创建完成就会将创建bean的ObjectFactory加入到缓存，
- 一旦下一个bean创建时需要依赖上个bean，就直接使用ObjectFactory.

## Bean 是线程安全的吗？

- 单例的bean不安全，prototype和request作用域的，安全。
- 通过无状态的设计实现线程安全。

## 创建bean的实例

- 初始化前先解析，如果已经创建了代理或者在初始化前的后处理器方法中改变了bean, 则直接返回就可以了。否则需要进行常规bean的创建。
- 创建过程包括：清除单例缓存，创建bean的实例(将BeanDefinition转换为BeanWrapper)，合并类定义的后处理器类解析父类和注解等，依赖处理，属性填充，检查循环依赖，注册DisposableBean, 完成创建并返回。
- 创建bean的实例，优先使用根定义类的工厂方法实例化，解析构造函数并构造实例。构造实例，要先检查缓存的构造器的唯一解析结果，没解析过的要重新先解析。然后对这个解析结果进行自动注入构造或者默认构造器构造(直接实例化)。
- 自动注入构造，初始化一个新的类包装器，依次从指定传参、根类定义缓存和配置中获取构造方法参数列表（并转换类型）和参数的个数，从指定传参或者反射获取构造器数组，按照构造器参数从多到少和公开优先的顺序排序，遍历解析构造器并加入缓存，参数类型转换，验证构造函数不是父类重写关系，根据实例化策略和构造函数与参数实例化bean.
- 实例化策略，如果没有使用replace(覆盖方法)或者lookup(动态替换)配置的方法，直接反射即可实例化。否则就需要使用cglib进行动态代理，将动态的拦截器增强切面方法织入类中，返回代理类。
- 记录创建bean的ObjectFactory。属性注入，包括根据根据名称、类型注入。
- 初始化bean，包括激活Aware三个方法，后处理器的前后使用，激活自定义的init方法。
- ApplicationContext是对BeanFactory的功能扩展，详见refresh()函数对AC的初始化：
- 准备刷新上下文环境（准备并验证系统属性或者环境变量），初始化FactoryBean并读取xml，填充FB的功能(如自动注入的注解)，开发者定制的子类覆盖方法(postProcessBeanFactory)执行，FB的后处理器执行，注册拦截bean创建的bean处理器（获取bean时调用），为上下文初始化Message国际化语言源，初始化应用消息广播器并AEM中，留给子类来初始化其他的bean, 在注册的bean中查找监听器bean并注册，初始化剩下的单例，完成刷新过程后，通知生命周期处理器刷新过程，同时发出上下文刷新时间通知其他类。
- 开发者定制的工厂类后处理方法，为类的创建提供了灵活性。

## Bean 的创建过程是什么？

- 根据class属性或名称解析类，通过override属性的同名方法个数验证合理性或者标记为没有重载方法，然后进行初始化前的预处理，创建bean.

- lookup-method和replace-method两个配置功能的加载就是设置到RootBeanDefinition的methodOverrides属性中。实现原理是在bean实例化时如果检测到存在methodOverrides属性，就会动态地为当前bean生成代理并使用对应的拦截器为bean作增强处理。

- 实例化的前置处理过程的bean经短路判断非空，则直接返回这个bean，忽略后续bean的创建。AOP功能就是基于这种判断。

## 如何从bean的实例中获取对象？

- 加载bean后通过getObjectForBeanInstance方法检测当前bean是否是FactoryBean类型，
- 是则调用该类型的工厂方法返回真正需要的bean实例，并进行后处理。

## spring 支持几种 bean 的作用域？

- spring 支持 5 种作用域，如下：
 - singleton：spring ioc 容器中只存在一个 bean 实例，bean 以单例模式存在，是系统默认值；
 - prototype：每次从容器调用 bean 时都会创建一个新的示例，既每次 getBean()相当于执行 new Bean()操作；
 - Web 环境下的作用域：
  - request：每次 http 请求都会创建一个 bean；
  - session：同一个 http session 共享一个 bean 实例；
  - global-session：用于 portlet 容器，因为每个 portlet 有单独的 session，globalsession 提供一个全局性的 http session。
- 注意： 使用 prototype 作用域需要慎重的思考，因为频繁创建和销毁 bean 会带来很大的性能开销。

## spring 自动装配 bean 有哪些方式？

- no：默认值，表示没有自动装配，应使用显式 bean 引用进行装配。
- byName：它根据 bean 的名称注入对象依赖项。
- byType：它根据类型注入对象依赖项。
- 构造函数：通过构造函数来注入依赖项，需要设置大量的参数。
- autodetect：容器首先通过构造函数使用 autowire 装配，如果不能，则通过 byType 自动装配。

# Spring 事务

## spring 事务实现方式有哪些？

- 声明式事务：声明式事务也有两种实现方式，基于 xml 配置文件的方式和注解方式（在类上添加 @Transaction 注解）。
- 程序化事务：提供编码的形式管理和维护事务。


## 哪种事务管理类型更可取？
- Spring Framework的大多数用户选择声明式事务管理，因为它是对应用程序代码影响最小的选项，因此最符合非侵入式轻量级容器的理想。
- 声明式事务管理优于程序化事务管理，但它不如程序化事务管理灵活，后者允许您通过代码控制事务。

## 说一下 spring 的事务隔离？

- spring 有五大隔离级别，默认值为 ISOLATION_DEFAULT（使用数据库的设置），其他四个隔离级别和数据库的隔离级别一致：

- ISOLATION_DEFAULT：用底层数据库的设置隔离级别，数据库设置的是什么我就用什么；

- ISOLATIONREADUNCOMMITTED：未提交读，最低隔离级别、事务未提交前，就可被其他事务读取（会出现幻读、脏读、不可重复读）；

- ISOLATIONREADCOMMITTED：提交读，一个事务提交后才能被其他事务读取到（会造成幻读、不可重复读），SQL server 的默认级别；

- ISOLATIONREPEATABLEREAD：可重复读，保证多次读取同一个数据时，其值都和事务开始时候的内容是一致，禁止读取到别的事务未提交的数据（会造成幻读），MySQL 的默认级别；

- ISOLATION_SERIALIZABLE：序列化，代价最高最可靠的隔离级别，该隔离级别能防止脏读、不可重复读、幻读。

- 脏读 ：表示一个事务能够读取另一个事务中还未提交的数据。比如，某个事务尝试插入记录 A，此时该事务还未提交，然后另一个事务尝试读取到了记录 A。

- 不可重复读 ：是指在一个事务内，多次读同一数据。

- 幻读 ：指同一个事务内多次查询返回的结果集不一样。比如同一个事务 A 第一次查询时候有 n 条记录，但是第二次同等条件下查询却有 n+1 条记录，这就好像产生了幻觉。发生幻读的原因也是另外一个事务新增或者删除或者修改了第一个事务结果集里面的数据，同一个记录的数据内容被修改了，所有数据行的记录就变多或者变少了。

## Spring Framework的事务管理有哪些好处？
- 它在不同的事务API（如JTA，JDBC，Hibernate，JPA和JDO）之间提供了一致的编程模型。 
- 与许多复杂的事务API（如JTA）相比，它为程序化事务管理提供了更简单的API。 
- 它支持声明式事务管理。 
- 它与Spring的各种数据访问抽象集成得非常好。

# Spring MVC

## 说一下 spring mvc 运行流程？

- spring mvc 先将请求发送给 DispatcherServlet。
- DispatcherServlet 查询一个或多个 HandlerMapping，找到处理请求的 Controller。
- DispatcherServlet 再把请求提交到对应的 Controller。
- Controller 进行业务逻辑处理后，会返回一个ModelAndView。
- Dispathcher 查询一个或多个 ViewResolver 视图解析器，找到 ModelAndView 对象指定的视图对象。
- 视图对象负责渲染返回给客户端。

## spring mvc 有哪些组件？

- 前置控制器 DispatcherServlet。
- 映射控制器 HandlerMapping。
- 处理器 Controller。
- 模型和视图 ModelAndView。
- 视图解析器 ViewResolver。

## @RequestMapping 的作用是什么？

- 将 http 请求映射到相应的类/方法上。

## @Autowired 的作用是什么？
- @Autowired 它可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作，
- 通过@Autowired 的使用来消除 set/get 方法。
