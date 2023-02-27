  

## 一、Spring介绍

### 简介

- Spring:春---->给软件行业带来了春天
- 2002，首次推出了Spring框架的雏形: interface21  框架
- Spring框架即以interface21框架为基础，经过重新设计，并不断丰富其内涵,于2004年3月24日发布了1.0正式版
- Rod Johnson，Spring Framework创始人，著名作者。很难想象Rod Johnson的学历，真的让好多人大吃一惊，他是悉尼大学音乐学的博士，然而他的专业不是计算机，而是音乐学
- spring理念: 使现有的技术更加容易使用，本身是一个大杂烩，**整合了现有的技术框架**
- SSH : Struct2 + Spring + Hibernate
- SSM：SpringMvc + Spring + Mybatis

官网: https://spring.io/projects/spring-framework#overview

 官方下载文档地址: http://repo.spring.io/release/org/springframework/spring

 GitHub: https://github.com/spring:projects/spring-framework

中文文档: https://www.docs4dev.com/docs/zh/spring-framework/5.1.3.RELEASE/reference



### 优点

- Spring 是一个开源免费的框架(容器)
- Spring 是一个轻量级的、非入侵式的框架
- 控制反转 (IOC) , 面向切边编程 (AOP)
- 支持事物的处理, 支持对框架的整合

> 总结:  Spring就是一个轻量级的 控制反转(IOC) 和面向切面编程(AOP) 的框架!



### 组成

![](Spring.assets/Spring%E6%A8%A1%E5%9D%97%E5%9B%BE.png)



### 拓展

现代化的Java开发都是基于SpringBoot的开发

- Spring Boot

  - 一个快速开发的脚手架
  - 基于SpringBoot 可以快速的开发单个微服务
  - 约定大于配置

- Spring Cloud

  - SpringCloud 是基于SpringBoot 实现的

    

现在大多数企业都使用SpringBoot进行快速开发, 学习SpringBoot的前提, 需要完全掌握Spring以及SpringMVC .   Spring有承上启下的作用

**Spring弊端:  因发展了太久之后, 配置十分繁琐, 人称: "配置地狱!!"**

 

## 二、⭐IOC理论推导



原来实现一个业务的步骤

1. UserDao 接口
2. UserDaoImple 实现类
3. UserService 业务接口
4. UserServiceImpl 业务实现类

在我们之前的业务中, 用户的需求可能会影响我们原来的代码, 我们需要根据用户的需求去修改源代码, 如果程序代码量十分大, 修改一次的成本价将十分昂贵!



我们使用一个set接口实现,  已经发生了革命性的变化!!!!

```java
 private UserDao userDao;

    //使用set 动态实现对象的注入
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
```

- 之前,   程序是主动创建对象!   控制权在程序员手上
- 使用了**set注入后, 程序不在具有主动性, 而是变成了被动的接受对象**!

​       这种思想, 从本质上解决了问题, 我们(程序员)不用再去管理对象的创建了. 系统的耦合性大大降低!!   可以更加的专注在业务的实现上.  这就是IOC的原型



### IOC本质

**控制反转IOC(Inversion of Control)，是一种设计思想，DI(依赖注入)是实现IOC的一种方法**，也有人认为DI只是IOC的另一种说法(错误)。没有IOC的程序中 , 我们使用面向对象编程 , 对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，所谓控制反转就是：**获得依赖对象的方式反转了**。

![](Spring.assets/IOC%E8%A7%A3%E8%80%A6.png)

**IOC是Spring框架的核心内容**，使用多种方式完美的实现了IOC，可以使用XML配置，也可以使用注解，新版本的Spring也可以零配置实现IOC。

`Spring IOC容器`在初始化时先读取配置文件，根据配置文件或元数据创建与组织对象存入容器中，程序使用时再从IOC容器中取出需要的对象。

![](Spring.assets/IOC%E5%AE%B9%E5%99%A8.png)

## 三、第一个Spring程序

### 环境准备

导入Spring依赖: 只需要导入webmvc即可, 其他的由于都依赖于webmvc,会自动导入

```xml
 <dependency>
     <groupId>org.springframework</groupId>
     <artifactId>spring-webmvc</artifactId>
     <version>5.2.0.RELEASE</version>
</dependency>
```



### 步骤

1. 建立一个新的子项目   spring-02-hellospring

2. 在com.xiaoyu.pojo包下编写一个hello类  有str属性, 并给get和set方法

   ```java
   public class Hello {
   
       String str;
   
       public String getStr() {
           return str;
       }
   
       public void setStr(String str) {
           this.str = str;
       }
   
       @Override
       public String toString() {
           return "Hello{" +
                   "str='" + str + '\'' +
                   '}';
       }
   }
   ```

   

3. 在resources 包下, 建立**beans.xml** 文件. 去官方文档下复制配置

    ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <!-- 使用Spring来创建对象 在Spring中这些对象都被称为bean-->
       <!-- id 为对象名  class new的对象 -->
       <bean id="hello" class="com.xiaoyu.pojo.Hello" >
           <!-- property 相当于给对象中的属性设置一个值!  -->
           <property name="str" value="hello, Spring!"/>
       </bean>
   </beans>
   ```

4. 测试

   ```java
   public class MyTest {
       public static void main(String[] args) {
   
           //获取Spring的上下文对象 context
           ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
   
           //我们的对象现在都在Spring中的管理了, 要使用, 直接去里面取出来就可以!
           Hello hello = (Hello) context.getBean("hello");
   
           System.out.println(hello);
       }
   }
   ```

   

### 思考

- Hello 对象是谁创建的 ?  
  - hello 对象是由Spring创建的
- Hello 对象的属性是怎么设置的 ?  
  - hello 对象的属性是由Spring容器设置的

这个过程就叫控制反转

- 控制 : 谁来控制对象的创建 , 传统应用程序的对象是由程序本身控制创建的 , 使用Spring后 , 对象是由Spring来创建的
- 反转 : **程序本身不创建对象 , 而变成被动的接收对象 .**

依赖注入 : 就是利用set方法来进行注入的.

### 修改案例一

对spring-01-base的修改

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="mysqlImpl" class="com.xiaoyu.dao.UserDaoMysqlImpl" />
    <bean id="oracleImpl" class="com.xiaoyu.dao.UserDaoOracleImpl" />

    <bean id="userServiceImpl" class="com.xiaoyu.service.UserServiceImpl" >
        <!-- ref: 引用Spring 中创建好的对象
             value: 具体的值, 基本数据类型   -->
        <property name="userDao" ref="oracleImpl"/>
    </bean>


</beans>
```

测试

```java
public class MyTest {
    public static void main(String[] args) {

        //获取ApplicationContext, 拿到Spring的容器
        ApplicationContext contest = new ClassPathXmlApplicationContext("beans.xml");

        //从Spring容器中获取对象
        UserService userServiceImpl = (UserService) contest.getBean("userServiceImpl");

        userServiceImpl.getUser();
    }
}
```



#### 小结



>  IOC是一种编程思想，由主动的编程变成被动的接收

> 所谓的IoC,一句话搞定 : 对象由Spring 来创建 , 管理 , 装配 !



## 四、IOC创建对象的方式

### 使用无参构造器创建对象

```xml
<bean id="username" class="com.xiaoyu.pojo.User" >
    <property name="username" value="小鱼"/>
</bean>
```



### 使用有参构造器创建对象

三种方式

1. 第一种方式: **下标赋值**

   ```xml
   <bean id="username" class="com.xiaoyu.pojo.User" >
       <constructor-arg index="0" value="李华" />
   </bean>
   ```

2. 第二种方式:  **类型赋值**

   ```xml
   <bean id="username" class="com.xiaoyu.pojo.User" >
       <constructor-arg type="java.lang.String" value="小鱼" />
   </bean>
   ```

3. 第三种方式: 通过**构造器的参数名赋值**

   ```xml
   <bean id="username" class="com.xiaoyu.pojo.User" >
       <constructor-arg name="username" value="小明" />
   </bean>
   ```

   

### 总结

在配置文件`beans.xml`加载的时候, 容器 `context`中管理的对象就应经初始化了!



## 五、✅Spring配置

### 别名 alias

对象的名称, 从spring容器中取出对象时, 可以通过别名来取出来

```xml
<alias name="username" alias="user" />
```

### Bean的配置

```xml
<bean id="username" class="com.xiaoyu.pojo.User" name="user2; user3, user4 user5" >
    <property name="username" value="小鱼"/>
</bean>
```

注意:  

- id 为对象名  
- class bean对象所对应的全限定名 包名 + 类名  
- name 起别名 可以有多个, 可以用, ; `&nbsp;` 来分隔

### Import

import一般用于团队开发使用,  可以将多个配置文件, 导入合并为一个

使用时,直接使用一个总的就可以

```xml
<import resource="beans.xml"/>
```



## 六、⭐依赖注入 DI

**依赖注入**(`Dependency Injection `)，是指程序运行过程中，如果需要调用另一个对象协助时，无须在代码中创建被调用者，而是**依赖**于外部的**注入**。



### 构造器注入

案例在上面



### ⭐set方式注入

- 依赖注入：Set注入！
  - 依赖 :   bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性，由容器来注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="address" class="com.xiaoyu.pojo.Address" >
        <property name="address" value="陕西西安"/>
    </bean>


    <bean id="student" class="com.xiaoyu.pojo.Student" >
        <property name="name" value="李华"/>
        <property name="address" ref="address"/>

        <!-- 数组-->
        <property name="book" >
            <array>
                <value>幻夜</value>
                <value>三体</value>
                <value>白夜行</value>
                <value>解忧杂货店</value>
            </array>
        </property>

        <!-- List集合 -->
        <property name="hobbys" >
            <list>
                <value>唱</value>
                <value>跳</value>
                <value>rap</value>
            </list>
        </property>

        <!-- map集合-->
        <property name="card">
            <map>
                <entry key="身份证" value="2022-1-1"/>
                <entry key="学生证" value="2201"/>
            </map>
        </property>

        <!-- Set集合-->
        <property name="games" >
            <set>
                <value>英雄联盟</value>
                <value>地下城与勇士</value>
            </set>
        </property>

        <!-- null -->
        <property name="wife">
            <null/>
        </property>

        <!-- properties-->
        <property name="info">
            <props>
                <prop key="driver">com.jdbc.mysql.Driver</prop>
                <prop key="url">jdbc://mysql</prop>
                <prop key="root">root</prop>
                <prop key="password">123456</prop>
            </props>
        </property>
    </bean>
</beans>
```



### 拓展方式注入

我们可以使用 p命名空间注入 和 c命名空间注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--p命名空间注入 可以直接注入属性的值: property -->
    <bean id="user" class="com.xiaoyu.pojo.User" p:name="小鱼" p:age="24" />

    <!-- c命名空间注入 通过构造器注入属性的值 construct-args -->
    <bean id="user2" class="com.xiaoyu.pojo.User" c:name="李华" c:age="18" />

</beans>
```



注意点: 

- p命名空间注入 和 c命名空间注入 不能直接使用, 要导入约束

  ```xml
  xmlns:p="http://www.springframework.org/schema/p"
  xmlns:c="http://www.springframework.org/schema/c"
  ```

  

### bean的作用域

|    Scope    | Description                                                  |
| :---------: | :----------------------------------------------------------- |
|  singleton  | (默认)将每个 Spring IoC 容器的单个 bean 定义范围限定为单个对象实例。 |
|  prototype  | 将单个 bean 定义的作用域限定为任意数量的对象实例。           |
|   request   | 将单个 bean 定义的范围限定为单个 HTTP 请求的生命周期。也就是说，每个 HTTP 请求都有一个在单个 bean 定义后面创建的 bean 实例。仅在可感知网络的 Spring `ApplicationContext`中有效。 |
|   session   | 将单个 bean 定义的范围限定为 HTTP `Session`的生命周期。仅在可感知网络的 Spring `ApplicationContext`上下文中有效。 |
| application | 将单个 bean 定义的范围限定为`ServletContext`的生命周期。仅在可感知网络的 Spring `ApplicationContext`上下文中有效。 |
|  websocket  | 将单个 bean 定义的范围限定为`WebSocket`的生命周期。仅在可感知网络的 Spring `ApplicationContext`上下文中有效。 |

#### 单例模式

默认为单例模式, 

```xml
<bean id="user" class="com.xiaoyu.pojo.User" p:name="小鱼" p:age="24" scope="singleton"/>
```

#### 原型模式

每次从容器中get得到的对象,  都会产生一个新的对象!

```xml
<bean id="user2" class="com.xiaoyu.pojo.User" scope="prototype">
    <property name="name" value="李华"/>
    <property name="age" value="18"/>
</bean>
```

#### request、session 、application

这些只能在web开发中使用



## 七、bean的自动装配

### 什么是自动装配

- 自动装配是Spring满足bean依赖的一种方式
- Spring会在上下文中自动寻找, 并自动给bean装配**引用属性!**



### Spring的三种装配方式

1. 在xml中显示的配置
2. 在java中显示配置
3. **隐式的自动装配 bean** 【重要】

#### ByName 自动装配

```xml
<bean id="cat" class="com.xiaoyu.pojo.Cat"/>
<bean id="dog" class="com.xiaoyu.pojo.Dog"/>

<!-- 使用自动装配, 自动为person中的cat和dog装配属性
     byName会自动在容器的上下文中查找, 和自己对象set方法后面的值对应  -->
<bean id="person" class="com.xiaoyu.pojo.Person" autowire="byName">
    <property name="name" value="小明"/>
</bean>
```



####  ByType自动装配

```xml
<bean id="cat" class="com.xiaoyu.pojo.Cat"/>
<bean id="dog" class="com.xiaoyu.pojo.Dog"/>

<!-- 使用自动装配, 自动为person中的cat和dog装配属性
        byType会自动在容器的上下文中查找, 和自己对象属性类型相同的bean -->
<bean id="person" class="com.xiaoyu.pojo.Person" autowire="byType">
    <property name="name" value="小明"/>
</bean>
```



#### 总结

- 使用byName时, 需要保证所有的bean的id唯一, 并且这个bean需要和自动注入的属性的set方法后的值一致
- 使用byType时, 需要保证所有bean的class唯一, 并且这个bean需要和自动注入的属性的类型一致



### ⭐使用注解实现自动装配 

#### 使用注解前的准备

1. 导入约束:  context约束
2. 配置注解的支持  `<context:annotation-config/>`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    
	<!--开启注解支持-->
    <context:annotation-config/>

</beans>
```



#### @Autowired

使用方法: 在需要自动配置bean的类的属性上使用即可, 也可以在set方法上使用

```java
public class People {
    @Autowired
    private Cat cat;
    @Autowired
    private Dog dog;
    private String name;
}
```



- `@Autowired` 默认为byType实现(若不满足, 会使用byName)

- 使用`@Autowired`我们可以不用编写Set方法了，前提是: 自动装配的属性在I0C (Spring) 容器中存在，且符合名字byname



`@Nullable`:  如果一个字段标记了这个注解, 说明资格字段可以为null



如果使用`@Autowired`时 自动装配的环境比较复杂, 自动装配无法完成时,  我们可以使用`@Qualifier(value="dog")`去配和`@Autowired`的使用, 指定一个唯一的id对象

```java
public class People {
    @Autowired
    private Cat cat;
    @Autowired
    @Qualifier(value = "dog")
    private Dog dog;
    private String name;
}
```

#### @Resource

`@Resource`也可以实现自动装配,  要注意的是: **默认为byName实现**(若不满足, 会使用byType)



#### `@Autowired`和`@Resource`的区别

- `@autowire`通过**byType(默认)**和byName实现，而且必须要求这个对象存在,  不存在配合`@Qualifier(value = "dog")` 使用
- `@resource`默认通过**byName(默认)**和byType实现，如果找不到，通过`@Resource(name="dog")`实现

## 八、使用注解开发

### 使用注解前准备

1. 使用注解前必须要导入context 约束, 并增加注解的支持
2. 指定要扫描的包，这个包下的注解就会生效

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    
	 <!-- 指定要扫描的包，这个包下的注解就会生效-->
    <context:component-scan base-package="com"/>
    <!--开启注解支持   因上面已使用 扫描包注解,  所以下面的可以省略-->
    <context:annotation-config/>

</beans>
```





### 注解的使用

#### 注册bean

```java
// @Component 相当于<bean id="user" class="com.xiaoyu.pojo.User"/> 
@Component
public class User {
    
    private String name;
    
}
```





#### 使用注解注入属性

使用方法: 在**属性上**或**set方法上**使用`@Value("小鱼")` 即可

```java
// @Component 相当于<bean id="user" class="com.xiaoyu.pojo.User"/>
@Component
public class User {

    // @Value("小鱼") 相当于<property name="name" value="小鱼"/>
    private String name;

    @Value("小鱼")
    public void setName(String name) {
        this.name = name;
    }
}
```





#### @Component衍生的注解

`@Component`有几个衍生注解，我们在web开发中，会按照MVC三层架构分层

- dao 【`@Repository`】

- service  【`@Service`】

- controller  【`@Controller`】

  

**这四个注解功能都是一样的，都是代表将某个类注册到Spring中，装配Bean对象**



#### 作用域

`@Scope`: 声明作用域的注解

```java
// 作用域
@Scope("singleton")
public class User {

    // @Value("小鱼") 相当于<property name="name" value="小鱼"/>
    @Value("小鱼")
    private String name;

}
```



#### 小结

xml与注解

- xml更加万能，维护简单
- 注解:   不是自己的类，使用不了，维护复杂

最佳实践：

- xml用来管理bean
- 注解只用来完成属性的注入
- 需要开启注解支持



## 九、使用java配置Spring

我们现在要完全不使用Spring的xml配置了，全权交给Java来做!

JavaConfig是Spring的一一个子项目，在Spring 4之后，它成为了一-个核心功能!



### 使用`@Bean`来注册 bean

1. 声明这个类为配置类, 使用`@Configuration`来完成
2. 在方法上使用`@Bean` 

  ```java

// @Configuration表示这是一个配置类, 相当于beans.xml
@Configuration

public class MyConfig {

    // @Bean 注册一个bean, 相当于在beans.xml中的一个 bean标签 <bean id="user" class="com.xiaoyu.pojo.User"/>
    // 这个方法名 相当于bean标签中的id属性  返回类型相当于class属性
    @Bean
    public User getUser(){
        return new User();
    }

}
  ```





```java
public class User {

    @Value("小鱼")
    private String name;

    @Value("20")
    private int age;
    
    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```



### 使用`@Component`来注册bean

1. 声明这个类为配置类, 使用`@Configuration`来完成

2. 使用`@ComponentScan`指定要扫描的包, 使这个包下的注解生效

   ```java
   
   // @Configuration表示这是一个配置类, 相当于beans.xml
   @Configuration
   
   // @ComponentScan  指定要扫描的包，这个包下的注解就会生效
   @ComponentScan("com.xiaoyu")
   public class MyConfig {
   }
   ```

   

3. 在实体类上声明`@Component("user")`

   ```java
   @Component("user")
   public class User {
   
       @Value("小鱼")
       private String name;
   
       @Value("20")
       private int age;
       
       public void setName(String name) {
           this.name = name;
       }
   
       public void setAge(int age) {
           this.age = age;
       }
   }
   ```

### 两种方式的测试

```java
public class MyTest {
    public static void main(String[] args) {

        ApplicationContext context = new 				       AnnotationConfigApplicationContext(MyConfig.class);

        User user = context.getBean("getUser", User.class);
        User user1 = (User) context.getBean("user");
        System.out.println(user == user1);

    }
}
```



### 总结

使用`@bean` 和`@Component`都能完成注册bean

- `@bean`相当于你在xml中写bean配置

- 也可以用`@component（"xx"）`前提要`@componentscan`开启扫描
- 取出时对象时, `@component（"xx"）`get的时候用xx这个名字，而`@bean`用的是get**方法名**字
- 如果两种方式同时使用, 会得到两个不同的对象



## 十、⭐代理模式

为什么要学习代理模式

- **SpringAOP的底层是代理模式**

代理模式的分类:

- 静态代理
- 动态代理



### 静态代理

**角色分析**

- 抽象角色:  一般会使用借考或者抽象类来解决
- 真实角色:  被代理的角色
- 代理角色:  代理真实角色, 代理真实角色后, 我们一般会做一些附属操作
- 客户:  访问代理对象的人

**案例:**

1. 接口

   ```java
   public interface Rent {
       void rent();
   }
   ```

   

2. 真实角色:  被代理的角色

   ```java
   public class Host implements Rent{
   
       @Override
       public void rent() {
           System.out.println("房东要出租房子");
       }
   }
   ```

   

3. 代理角色

   ```java
   public class Proxy implements Rent {
   
       private Host host;
   
       public Proxy() {
       }
   
       public Proxy(Host host) {
           this.host = host;
       }
   
       @Override
       public void rent() {
           seeHouse();
           host.rent();
           fare();
       }
   
       public void seeHouse(){
           System.out.println("中介带你去看房子");
       }
   
       public void fare(){
           System.out.println("中介收取中介费");
       }
   }
   ```

   

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
   
           //房东要出租房子
           Host host = new Host();
   
           //代理, 中介帮房东租房子, 但是代理一般会有一些附属操作
           Proxy proxy = new Proxy(host);
   
           //不用面对房东, 只需要找中介就可以了
           proxy.rent();
       }
   }
   ```

   

 **代理模式的好处**

- 可以使真实角色的操作更加纯粹! 不用去关注一些公共的业务
- 公共业务也就交给了代理角色, 实现了业务的分工
- 公共业务发生拓展的时候, 方便集中管理

缺点: 

一个真实角色就会产生一个代理角色,  代码量会翻倍, 降低开发效率



### 静态代理的再理解

![](Spring.assets/AOP%E9%9D%A2%E5%90%91%E5%88%87%E9%9D%A2%E7%90%86%E8%A7%A3%E5%9B%BE.png)

**案例二**

1. 接口

   ```java
   public interface UserService {
   
       void add();
   
       void delete();
   
       void update();
   
       void query();
   
   }
   ```

   

2. 真实角色:  被代理的角色

   ```java
   public class UserServiceImpl implements UserService{
   
       @Override
       public void add() {
           System.out.println("添加了一个用户");
       }
   
       @Override
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       @Override
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       @Override
       public void query() {
           System.out.println("查询了一个用户");
       }
   }
   ```

   

3. 代理角色

   ```java
   public class UserServiceProxy implements UserService {
   
       private UserServiceImpl userService;
   
       public void setUserService(UserServiceImpl userService) {
           this.userService = userService;
       }
   
       @Override
       public void add() {
           log("add");
           userService.add();
       }
   
       @Override
       public void delete() {
           log("delete");
           userService.delete();
       }
   
       @Override
       public void update() {
           log("update");
           userService.update();
       }
   
       @Override
       public void query() {
           log("query");
           userService.query();
       }
   
       public void log(String msg){
           System.out.println("info: 使用了" + msg + "方法");
   
       }
   }
   ```

   

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
   
           UserServiceImpl userService = new UserServiceImpl();
   
           UserServiceProxy userServiceProxy = new UserServiceProxy();
           userServiceProxy.setUserService(userService);
   
           userServiceProxy.add();
       }
   }
   ```

   **在不破坏原有代码的基础上，利用“织入”的模式来实现代码的动态配置**



### ⭐动态代理

#### 动态代理介绍

动态代理的角色和静态代理的一样 .

**动态代理的代理类是动态生成的 . 静态代理的代理类是我们提前写好的**

动态代理分为两类 : 一类是基于接口动态代理 , 一类是基于类的动态代理

- 基于接口的动态代理---**-JDK动态代理**


- 基于类的动态代理--cglib


现在用的比较多的是 javasist 来生成动态代理 (了解),  我们这里**使用JDK的原生代码**来实现，其余的道理都是一样的！



**JDK的动态代理需要了解两个类**

-  InvocationHandler   【InvocationHandler：调用处理程序】
-  Proxy   打开JDK帮助文档查看



#### 案例一

接口

```java
public interface Rent {

    void rent();
}
```

真实角色

```java
public class Host implements Rent {

    @Override
    public void rent() {
        System.out.println("房东要出租房子");
    }
}
```

**处理程序 (动态代理核心类)**

```java
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口()
    private Rent rent;

    //生成得到代理对象
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                                      rent.getClass().getInterfaces(),this);
    }


    //处理代理实例, 并返回结果
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        Object result = method.invoke(rent, args);
        return result;

    }

    public void setRent(Rent rent) {
        this.rent = rent;
    }
}

```

客户端访问

```java
public class Client {
    public static void main(String[] args) {

        //真实角色
        Rent rent = new Host();

        ProxyInvocationHandler pih = new ProxyInvocationHandler();
        pih.setRent(rent);

        Rent proxy = (Rent) pih.getProxy();
        proxy.rent();
    }
}

```





#### 案例二

1. 接口

   ```java
   public interface UserService {
   
       void add();
   
       void delete();
   
       void update();
   
       void query();
   
   }
   ```

   

2. 真实角色

   ```java
   public class UserServiceImpl implements UserService{
   
       @Override
       public void add() {
           System.out.println("添加了一个用户");
       }
   
       @Override
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       @Override
       public void update() {
           System.out.println("修改了一个用户");
       }
   
       @Override
       public void query() {
           System.out.println("查询了一个用户");
       }
   }
   ```

3. **处理程序 (动态代理核心类,通用的动态代理实现的类)**

   ```java
   /**
    * @author 小鱼
    * @version 1.0
    * 自动生成代理对象
    */
   public class ProxyInvocationHandler implements InvocationHandler {
   
       //被代理的接口
       private Object target;
   
       //生成得到代理对象
       public Object getProxy(){
           return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                   target.getClass().getInterfaces(),this);
       }
   
       //处理代理实例, 并返回结果
       @Override
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
   
           log(method.getName());
           return method.invoke(target, args);
       }
   
       public void log(String msg) {
           System.out.println("[info]: 进入了"+ msg + "方法");
       }
   
   
       public void setTarget(Object target) {
           this.target = target;
       }
   }
   
   ```

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
           UserServiceImpl userService = new UserServiceImpl();
   
           ProxyInvocationHandler proxyInvocationHandler = new ProxyInvocationHandler();
           proxyInvocationHandler.setTarget(userService);
   
           UserService proxy = (UserService) proxyInvocationHandler.getProxy();
           proxy.delete();
   
       }
   }
   ```

spring - 08 -proxy -demo05 有较容易理解的案例!!!



#### 处理程序的理解

- `getProxy()` 方法得到**动态代理类的实例**, 这个类实现了需要代理的接口, 并重写了方法
- `invoke()` 会通过反射 得到需要执行的具体方法



### 总结

**一个动态代理 , 一般代理某一类业务 , 一个动态代理可以代理多个类，代理的是接口！**

动态代理的好处: 

- 可以使真实角色的操作更加纯粹!不用去关注一-些公共的业务
- 公共也就就交给代理角色!实现了业务的分工!
- 公共业务发生扩展的时候，方便集中管理!
- 一个动态代理类代理的是一一个接口，一 -般就是对应的一类业务
- **一个动态代理类可以代理多个类，只要是实现了同一个接口即可!**



## 十一、AOP

### 什么是AOP

**AOP (Aspect Oriented Programming)**意为:**面向切面编程**,通过预编译方式和运行期动态代理实现程序功能
 的统一维护的一 -种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一重要内容,是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得**业务逻辑各部分之间的耦合度降低，提高程序的可重用性,同时提高了开发的效率**。

![](Spring.assets/AOP%E7%9A%84%E7%90%86%E8%A7%A3.png)

### AOP在Spring中的应用

**提供声明式事务：允许用户自定义切面**

以下名词需要了解：

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如**日志 , 安全 , 缓存 , 事务**等等 ....


- 切面（ASPECT）：横切关注点 被模块化 的特殊对象。即，它是一个类。**【增强功能的类】**


- 通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法。**【增强的功能】**


- 目标（Target）：被通知对象。**【需要切入的类/对象】**


- 代理（Proxy）：向目标对象应用通知之后创建的对象。


- 切入点（PointCut）：切面通知 执行的 “地点”的定义。


- 连接点（JointPoint）：与切入点匹配的执行点



![](Spring.assets/%E9%9D%A2%E5%90%91%E5%88%87%E9%9D%A2%E7%90%86%E8%A7%A3%E5%9B%BE.png)

SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice:

![](Spring.assets/Spring%E4%B8%AD5%E4%B8%AD%E7%B1%BB%E5%9E%8B%E7%9A%84advice.png)

**即 Aop 在 不改变原有代码的情况下 , 去增加新的功能**



### 使用Spring实现AOP

#### 使用Spring实现AOP前的准备

使用AOP织入, 需要导入一个依赖包

```xml
<!-- aop织入包 -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```



#### 方式一: 使用Spring的API接口

**【主要是: Spring的接口实现】**

1. 编写接口类和实现类

   ```java
   public interface UserService {
       
       void add();
   
       void update();
   
       void delete();
   
       void select();
   }
   ```

   

   ```java
   public class UserServiceImpl implements UserService {
   
       @Override
       public void add() {
           System.out.println("新增了一个用户");
       }
   
       @Override
       public void update() {
           System.out.println("更新了一个用户");
       }
   
       @Override
       public void delete() {
           System.out.println("删除了一个用户");
       }
   
       @Override
       public void select() {
           System.out.println("查询了一个用户");
       }
   }
   ```

2. 编写增强类,  我们编写两个, 一个前置增强, 一个后置增强

   ```java
   public class Log  implements MethodBeforeAdvice {
   
       /**
        *
        * @param method 要执行的目标对象的方法
        * @param args 参数
        * @param target 目标对象
        */
       @Override
       public void before(Method method, Object[] args, Object target) throws Throwable {
   
           assert target != null;
           System.out.println(target.getClass().getName() + "的" +  method.getName() + "方法被执行了");
       }
   }
   ```

   后置增强类

   ```java
   public class LogAfter implements AfterReturningAdvice {
   
       /**
        *
        * @param returnValue 执行方法后返回的值
        * @param method 执行的方法
        * @param args 参数
        * @param target 目标对象
        */
       @Override
       public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
           System.out.println("执行了" + method.getName() + "方法" + "返回值为" + returnValue);
       }
   }
   ```

3. **去Spring 的 配置文件中注册,  并实现aop切入实现 , 注意导入约束 .**

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/aop
           https://www.springframework.org/schema/aop/spring-aop.xsd">
   
       <!-- 注册bean -->
       <bean id="userService" class="com.xiaoyu.service.UserServiceImpl"/>
       <bean id="log" class="com.xiaoyu.log.Log"/>
       <bean id="afterLog" class="com.xiaoyu.log.LogAfter"/>
   
   
       <!-- 配置aop -->
       <aop:config>
           <!-- pointcut: 切入点  expression: 表达式 execution(要执行的位置)-->
           <!-- 修饰符 返回值 全限定类名 方法名 参数 -->
           <aop:pointcut id="pointcut" expression="execution(public * com.xiaoyu.service.UserServiceImpl.*(..) )" />
   
           <!-- 执行环绕增加 -->
           <!-- 可以理解为: 把log和 afterLog 的方法切入到userServiceImpl 这个类中的方法 -->
           <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
           <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
       </aop:config>
   </beans>
   ```
   
4. 测试

   ```java
   public class MyTest {
       public static void main(String[] args) {
   
           ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
   
           // 注意: 这里返回的是代理类实例  代理的是接口
           UserService userService = (UserService) context.getBean("userService");
           userService.add();
   
       }
   }
   ```

导入aop约束的快捷方法: 输入`<aop:config`  IDEA会自动导入 

关于`expression`表达式: 

- `execution(修饰符  返回值  包名.类名/接口名.方法名(参数列表))`
- (..)可以代表所有参数,()代表一个参数,(,String)代表第一个参数为任何值,第二个参数为String类型.

#### 方式二: 自定义类实现AOP

**【主要是切面的自定义】**

目标业务类不变依旧是userServiceImpl

1. 写一个我们自定义的切面类

   ```java
   public class DiyPointCut {
   
       public void before() {
           System.out.println("====执行方法前====");
       }
   
       public void after() {
           System.out.println("====执行方法后====");
       }
   }
   ```

2. 去Spring中配置

   ```xml
   <!-- 方式二: 自定义类实现AOP -->
   <bean id="diy" class="com.xiaoyu.diy.DiyPointCut"/>
   <aop:config>
       <!-- 自定义的切面 ref 要引用的类 -->
       <aop:aspect ref="diy" >
           <!-- 切点-->
           <aop:pointcut id="pointcut" expression="execution(public * com.xiaoyu.service.UserServiceImpl.*(..) )"/>
   
           <!-- 通知 -->
           <aop:before method="before" pointcut-ref="pointcut"/>
           <aop:after method="after" pointcut-ref="pointcut"/>
   
       </aop:aspect>
   </aop:config>
   ```

3. 测试

   ```java
   public class MyTest {
       public static void main(String[] args) {
   
           ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
   
           // 注意: 这里返回的是代理类实例  代理的是接口
           UserService userService = (UserService) context.getBean("userService");
           userService.add();
       }
   }
   ```
   


#### 方式三: 使用注解实现AOP

使用注解实现AOP前的准备: 

- 在Spring的配置文件中声明:   开启注解实现AOP的支持 

  ```xml
  <aop:aspectj-autoproxy/>
  ```

步骤说明: 

第一步: 编写一个注解实现的切面类  并注册bean   注意: 

```java
@Component  //注册bean
@Aspect //声明此类为切面类
public class AnnotationPointcut {

    @Before("execution(public * com.xiaoyu.service.UserServiceImpl.*(..) )")
    public void before() {
        System.out.println("====执行方法前====");
    }

    @After("execution(public * com.xiaoyu.service.UserServiceImpl.*(..) )")
    public void after() {
        System.out.println("====执行方法前====");
    }

    @Around("execution(public * com.xiaoyu.service.UserServiceImpl.*(..) )")
    public void around(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("环绕前");

        joinPoint.proceed();

        System.out.println("环绕后");
    }
}
```

注意点: 

- 不要导错包  `import org.aspectj.lang.annotation.Before;`
- 如果使用注解来注册bean  需要开启包扫描`<context:component-scan base-package="com"/>`     指定要扫描的包，这个包下的注解就会生效

第二步: 测试

```java
public class MyTest {
    public static void main(String[] args) {

        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        // 注意: 这里返回的是代理类实例  代理的是接口
        UserService userService = (UserService) context.getBean("userService");
        userService.add();

    }
}
```

- 关于环绕、before after的执行顺序    Spring5.20版本
  - 正常情况：环绕前置=====@Before=====目标方法执行=====@AfterReturning=====@After=====环绕返回=====环绕最终
  - 异常情况：环绕前置=====@Before=====目标方法执行=====@AfterThrowing=====@After=====环绕异常=====环绕最终

- 关于 aop:aspectj-autoproxy 的说明

  - 命名空间的`<aop:aspectj-autoproxy />`声明自动为spring容器中那些配置@aspectJ切面的bean创建代理，织入切面。当然，spring 在内部依旧采用AnnotationAwareAspectJAutoProxyCreator进行自动代理的创建工作，但具体实现的细节已经被<aop:aspectj-autoproxy />隐藏起来了
- `<aop:aspectj-autoproxy />`有一个proxy-target-class属性，默认为false，表示使用jdk动态代理织入增强，当配为<aop:aspectj-autoproxy  poxy-target-class="true"/>时，表示使用CGLib动态代理技术织入增强。不过即使proxy-target-class设置为false，如果目标类没有声明接口，则spring将自动使用CGLib动态代理



## 十二、整合Mybatis

### 整合Mybatis的准备

1. 使用maven导入相关jar包

   - spring
   - mybatis
   - MySQL驱动
   - spring-mybatis
   - aop织入包
   - junit单元测试
   - lombot 
   - spring-jdbc  

2. 编写配置文件

3. 测试

   

### Mybatis-Spring

#### 方式一

1. 编写数据源配置

2. sqlSessionFactory

3. SqlSessionTemplate

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd ">
   
       <!-- 注册bean-->
       <!-- 使用Spring的数据源来 代替mybatis的 dataSource数据源  也可使用其他数据源 如c3p0 druid dbcp-->
       <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
           <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
           <property name="url" value="jdbc:mysql://localhost:3306/exercise?useUnicode=true&amp;characterEncoding=UTF-8"/>
           <property name="username" value="root"/>
           <property name="password" value="123456"/>
       </bean>
   
       <!-- sqlSessionFactory -->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="dataSource" ref="dataSource"/>
           <!-- 绑定mybatis 配置文件-->
           <property name="configLocation" value="classpath:mybatis-config.xml"/>
       </bean>
       
       <!-- sqlSession -->
       <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
           <constructor-arg index="0" ref="sqlSessionFactory"/>
       </bean>
   
   </beans>
   ```
   

   
4. 需要给接口增加实现类

   ```java
   public class StuMapperImpl implements StuMapper{
   
       // SqlSessionTemplate 对象和 SqlSession 对象功能相同, 但SqlSessionTemplate 是线程安全的
       private SqlSessionTemplate sqlSession;
   
       @Override
       public List<Stu> getStuList() {
           return sqlSession.getMapper(StuMapper.class).getStuList();
       }
   
       public void setSqlSession(SqlSessionTemplate sqlSession) {
           this.sqlSession = sqlSession;
       }
   }
   ```

   

5. 将自己写的实现类, 注入到Spring

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           https://www.springframework.org/schema/beans/spring-beans.xsd">
   
   
       <!-- 导入spring-dao.xml 和此文件合并 -->
       <import resource="spring-dao.xml"/>
   
       <bean id="stuMapperImpl" class="com.xiaoyu.mapper.StuMapperImpl" >
           <property name="sqlSession" ref="sqlSession"/>
       </bean>
   
   </beans>
   ```

   

6. 测试使用

   ```java
   @Test
   public void query() {
   
       ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
       StuMapper stuMapperImpl = context.getBean("stuMapperImpl", StuMapper.class);
   
       for (Stu stu : stuMapperImpl.getStuList()) {
           System.out.println(stu);
       }
   }
   ```

   

#### 方式二

可以不用配置sqlSession, 改为实现类继承`SqlSessionDaoSupport`,  在注册实现类的bean时, 注入属性

```xml
 <bean id="stuMapperImpl2" class="com.xiaoyu.mapper.StuMapperImpl2">
     <property name="sqlSessionFactory" ref="sqlSessionFactory" />
</bean>
```



## 十三、声明式事务

### 回顾事务

- 把一组业务当成一个业务来做，要么成功，要么失败
- 事务在项目开发，十分的重要，涉及到数据的一致性问题
- 确保完整性和一致性

事务的ACID原则：

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源，防止数据损坏
- 持久性
  - 事务一旦提交，无论系统发生什么问题，结果都不会被影响，被持久化写到存储器中

### Spring中的事务管理

- 声明式事务：AOP
- 编程式事务：需要在代码中，进行事务管理

思考:
 为什么需要事务?

- 如果不配置事务，可能存在数据提交不一致的情况下;
- 如果我们不在SPRING中去配置声明式事务,我们就需要在代码中手动配置事务!
- 事务在项目的开发中十分重要，设计到数据的一致性和完整性问题，非常重要!



### 使用声明式事务

配置声明事务

```xml
<!-- 配置声明事务 注册 DataSourceTransactionManager 来实现事务管理-->
<bean id="transactionManage" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource"/>
</bean>

<!-- 结合AOP 实现事务的织入 -->
<!-- 配置事务通知 -->
<tx:advice id="txAdvice" transaction-manager="transactionManage" >
    <!-- 给那些方法配置事务 -->
    <!-- propagation: 事务的传播特性 -->
    <tx:attributes>
        <tx:method name="insert" propagation="REQUIRED"/>
        <tx:method name="*" propagation="REQUIRED"/>
        <tx:method name="query" read-only="true"/>
    </tx:attributes>
</tx:advice>


<!-- 配置事务切入-->
<aop:config>
    <aop:pointcut id="txPointCut" expression="execution(public * com.xiaoyu.dao.*.*(..) )"/>

    <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
</aop:config>
```



测试

```java
public class StuMapperImpl implements StuMapper {

    // SqlSessionTemplate 对象和 SqlSession 对象功能相同, 但SqlSessionTemplate 是线程安全的
    private SqlSessionTemplate sqlSession;

    public List<Stu> getStuList() {

        StuMapper mapper = sqlSession.getMapper(StuMapper.class);
        Stu stu = new Stu(8, "黑亮", 20, "男");

        mapper.insert(stu);
        int i = 1 / 0;

        mapper.delete(6);
        return mapper.getStuList();

    }

    public int insert(Stu stu) {
        return sqlSession.getMapper(StuMapper.class).insert(stu);
    }

    public int delete(int id) {
        return sqlSession.getMapper(StuMapper.class).delete(id);
    }

    public void setSqlSession(SqlSessionTemplate sqlSession) {
        this.sqlSession = sqlSession;
    }
}
```







