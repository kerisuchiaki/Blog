---
title: jvm学习笔记-常量池
date: 2023-10-01 15:29:25
tags: jvm
---

# 引入

思考下面的代码

```java
package com.yuyonghai;

public class Demo_2 {
    public static void main(String[] args) {
        String s=new String("a")+new String("b");
        System.out.println(System.identityHashCode(s));

        String str=s;
        System.out.println(System.identityHashCode(str));

        System.out.println(s==str);
                 str=s.intern();
        System.out.println("-----------");
        System.out.println(System.identityHashCode("ab"));

        System.out.println(System.identityHashCode(s));
        System.out.println(System.identityHashCode(str));//为什么str的内存地址没改变

        System.out.println(s=="ab");
        System.out.println(s==str);

    }
}

```

结果为：

```
460141958
460141958
true
-----------
460141958
460141958
460141958
true
true
```

为什么调用intern（）后str的内存地址没有指向常量池的"ab"实例？

# 常量池

常量池是字节码文件中的一个重要部分，存储了各种常量的信息，例如字符串、类引用、方法引用等

# intern()函数

- intern方法：native 方法，调用此方法时，如果池中已经包含等于此对象值的字符串，就返回池中的字符串；否则，将返回的引用指向当前的字符串；1.6版本需要将当前对象复制一份到池中，1.7后如果字符串常量池中没有的话，也不会在字符串常量池中创建新的示例而是直接指向堆中的实例，即常量池中的为类引用

