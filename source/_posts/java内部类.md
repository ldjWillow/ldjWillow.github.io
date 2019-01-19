---
title: java内部类
copyright: true
date: 2019-01-19 21:50:43
categories: [java]
tags: [java,static,内部类]
---

Java 语言中可以定义一个静态类吗？

答案是显而易见的：**YES** ，Java 语言存在静态类。

我们都知道，Java 语言中存在 **静态变量** 、存在 **静态方法** 、也存在 [静态块](https://www.twle.cn/t/445#reply0)。其实，Java 语言还存在 **静态类**。

## Java 语言中的静态类

[Java](https://www.twle.cn/l/yufei/java/java-basic-index.html) 语言允许我们在一个类中定义另一个类。类中的类我们称之为嵌套类。而包含嵌套类的类，我们则称之为 **外部类**。

Java 语言中，我们不能定义顶级的外部静态类。但我们可以定义静态的内部嵌套类。

也就是说，我们不能定义下面这中形式的静态类

```java
public static class JavaTester
{
}
```

当我们可以在类中定义一个静态的嵌套类，比如

```jav
public class JavaTester
{
    static class NestedStaticClass
    {
    }
}
```

那么，你会不会有另一个疑问：**静态和非静态的嵌套类有什么区别呢** ？

对了，忘记说了，**非静态嵌套类也被称为内部类**

## 静态和非静态的嵌套类的区别

静态嵌套类和非静态嵌套类的区别好多条，我们陈述下几个主要的区别：

1. 静态嵌套类使用时并不需要引用外部类。但非静态嵌套类 (内部类) 则必须引用外部类。
2. 非静态嵌套类(内部类) 可以访问外部类的静态和非静态成员。但静态嵌套类只能访问到外部类的静态成员，不可以访问外部类的非静态成员（实例成员）。
3. 非静态嵌套类(内部类) 不能单独实例化。必须先实例化外部类，才能实例化内部类。内部类可以引用外部类的数据和方法。因此，我们并不需要将外部类的引用传递给内部类的构造方法。这种机制，使得内部类更加简单明了。

## 范例

我们写一个范例来演示下静态嵌套类和非静态嵌套类的区别

```java
package com.noblelift.imp.products.mes.service.ifs.wcs;

public class JavaTester
{ 
   private static String msg = "简单教程，简单编程"; 

   // 静态嵌套类
   public static class NestedStaticClass{ 

       // 静态嵌套类只能访问外部类的静态成员  
       public void printMessage()
       { 

         // 如果将 msg 变量设为非静态的，则下面的语句会报错
         System.out.println("Message from nested static class: " + msg);  
       } 
    } 

    // 非静态嵌套类，也称之为内部类
    public class InnerClass{ 

       // 嵌套类可以访问外部类的静态和非静态成员 
       public void display(){ 
          System.out.println("Message from non-static nested class: "+ msg); 
       } 
    } 

    // 如何创建静态嵌套类和内部类的实例？
    public static void main(String args[]){ 

       // 创建一个静态嵌套类的实例
       JavaTester.NestedStaticClass printer = new JavaTester.NestedStaticClass(); 

       // 调用静态嵌套类的成员方法 
       printer.printMessage();    

       // 为了创建一个内部类的实例，我们必须先创建一个外部类的实例
       // 然后再创建内部类的时候
       JavaTester outer = new JavaTester();         
       JavaTester.InnerClass inner  = outer.new InnerClass(); 

       // 调用内部类的非静态成员 
       inner.display(); 

       // 我们可以将上面的两步合并为一步 
       JavaTester.InnerClass innerObject = new JavaTester().new InnerClass(); 

       // 现在，我们可以调用内部类的方法
       innerObject.display(); 
    } 
}

```

### 参考链接

[JAVA静态类](https://www.twle.cn/t/447)