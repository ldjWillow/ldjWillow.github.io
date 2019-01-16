---
title: Spring配置数据库方式
copyright: true
date: 2019-01-15 20:53:18
categories: Spring
tags: [Spring,数据库]
---

Spring中提供了多种不同形式的数据源配置方式

- Spring自带的数据源(DriverMangerDataSource)
- DBCP数据源
- C3P0数据源
- Druid数据源
- JNDI数据源

<!--more-->

所有数据源的jar包[下载地址1](http://www.java2s.com/Code/Jar/c/Catalogc.htm)[下载地址2](https://mvnrepository.com/artifact/org.apache.commons/commons-pool2?repo=redhat-earlyaccess)

下面简单介绍4种配置方式

####  DriverMangerDataSource :

说明：DriverManagerDataSource建立连接是只要能建立连接就新建一个connection，根本没有连接池的概念。

```xml
//id可以随便命名，如dataSource
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName"  value="com.mysql.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://localhost:3306/dbname" />
    <property name="username" value="root" />
    <property name="password" value="123456" />
</bean>  
```

####  DBCP

 DBCP的配置依赖于2个jar包commons-dbcp.jar，commons-pool.jar。

```xml
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
    <property name="driverClassName"  value="com.mysql.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://localhost:3306/dbname" />
    <property name="username" value="root" />
    <property name="password" value="123456" />
</bean>  
```

#### C3P0数据源

 C3P0是一个开放源代码的JDBC数据源实现项目，C3P0依赖于jar包c3p0.jar。

```xml
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">
   <!-- c3p0这个地方叫driverClassName -->
  <property name="driverClass"  value="com.mysql.jdbc.Driver" />
  <!-- c3p0这个地方叫url-->
  <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/dbname" />
  <!-- c3p0这个地方叫username-->
  <property name="user" value="root" />
  <property name="password" value="123456" />
</bean>
```

####  Druid数据源

```
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
    <property name="driverClassName"  value="com.mysql.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://localhost:3306/dbname" />
    <property name="username" value="root" />
    <property name="password" value="123456" />
</bean>  
```

[JNDI数据源的配置](https://www.cnblogs.com/xdp-gacl/p/3951952.html)

#### 参考链接

[几种数据源区别](https://blog.csdn.net/qq_34359363/article/details/72763491)

[Spring配置数据源的格式](https://www.cnblogs.com/zhc-hnust/p/4804125.html)

[Druid的Github地址](https://github.com/alibaba/druid/wiki/%E9%A6%96%E9%A1%B5)

[dbcp配置-官方文档中文版](http://www.blogjava.net/aoxj/archive/2008/02/19/180704.html)

[DBCP连接池配置](https://blog.csdn.net/god_v/article/details/80656827)

