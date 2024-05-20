---
title: spring学习笔记-拦截器与过滤器的区别
date: 2023-10-26 20:30:39
tags: spring
---

# 过滤器与拦截器的区别

区别主要体现一下5点：

1. 出身不同；
2. 触发时机不同；
3. 实现不同；
4. 支持的项目类型不同；
5. 使用的场景不同。

接下来，我们一一来看。

## 1.出身不同

过滤器来自于 Servlet，而拦截器来自于 Spring 框架，从上面代码中我们也可以看出，过滤器在实现时导入的是 Servlet 相关的包，如下图所示： 

<!-- more -->

![image.png](https://ask.qcloudimg.com/http-save/yehe-1740031/d7713f626b6ee4f41955e464d4fe9a7f.png)

image.png

 而拦截器在实现时，导入的是 Spring 相关的包，如下图所示： 

![image.png](https://ask.qcloudimg.com/http-save/yehe-1740031/6e2b33d3a4df496bc09de28d9df68093.png)

image.png

## 2.触发时机不同

**请求的执行顺序是：请求进入容器 > 进入过滤器 > 进入 Servlet > 进入拦截器 > 执行控制器（Controller）**，如下图所示： 

![image.png](https://ask.qcloudimg.com/http-save/yehe-1740031/b9d01a260af697502076b51dfc03162e.png)

image.png

 所以过滤器和拦截器的执行时机也是不同的，**过滤器会先执行，然后才会执行拦截器，最后才会进入真正的要调用的方法**。

## 3.实现不同

**过滤器是基于方法回调实现的**，我们在上面实现过滤器的时候就会发现，当我们要执行下一个过滤器或下一个流程时，需要调用 FilterChain 对象的 doFilter 方法进行回调执行，如下图所示： 

![image.png](https://ask.qcloudimg.com/http-save/yehe-1740031/f13f9002027ec84b68f67d88b9080cf4.png)

image.png

 由此可以看出，过滤器的实现是基于方法回调的。 而**拦截器是基于动态代理（底层是反射）实现的**，它的实现如下图所示： 

![image.png](https://ask.qcloudimg.com/http-save/yehe-1740031/3b4dac6564c9c1ffd5cd1cac658c7224.png)

image.png

 代理调用的效果如下图所示： 

![image.png](https://ask.qcloudimg.com/http-save/yehe-1740031/459e3e208802ff71643cda479e8e458b.png)

image.png

## 4.支持的项目类型不同

过滤器是 Servlet 规范中定义的，所以**过滤器要依赖 Servlet 容器，它只能用在 Web 项目中**；而**拦截器是 Spring 中的一个组件，因此拦截器既可以用在 Web 项目中，同时还可以用在 Application 或 Swing 程序中**。

## 5.使用的场景不同

因为拦截器更接近业务系统，所以**拦截器主要用来实现项目中的业务判断的**，比如：登录判断、权限判断、日志记录等业务。 而**过滤器通常是用来实现通用功能过滤的**，比如：敏感词过滤、字符集编码设置、响应数据压缩等功能。

## 总结

过滤器和拦截器都是基于 AOP 思想实现的，用来处理某个统一的功能的，但二者又有 5 点不同：出身不同、触发时机不同、实现不同、支持的项目类型不同以及使用的场景不同。过滤器通常是用来进行全局过滤的，而拦截器是用来实现某项业务拦截的。
