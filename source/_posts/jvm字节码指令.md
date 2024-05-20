---
title: jvm字节码指令
date: 2023-10-04 02:36:45
tags: 笔记
---

# jvm的字节码指令

## 关于try-catch-finaly关键代码块

当我们用try-catch-finaly关键代码块包裹起来时，生成的class文件里方法的code属性会会多一个ExceptionTable子属性，这个子属性记录发生异常的代码块和要捕捉的异常类和要执行的代码块

## 注意

不要在catch-fianly块中写return语句，不然字节码的指令会省略掉athrow命令即不会抛出异常，可能是编译的规则是人如果要执行的语句为return则省略后面的语句，毕竟执行不到，这会使得我们无法察觉到代码中发生的异常，这很危险
