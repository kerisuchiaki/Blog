---
title: git初始化一个项目
date: 2023-10-27 23:04:22
tags: git
---

# Git学习笔记

## 前言

记录常用的操作，免得还要上网搜

<!--more-->

## 一、本地初始化

> cd到对应的项目路径下，打开bash。增对这里有很多很多的操作，例如cmd,ps,cmder,bash等等

```bash
git init
1
```

这时候就会出现一个隐藏的 .git文件夹。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200301192753335.png)

## 二、 查看本地文件状态

```bash
git status
1
```

这时就会看到有一个新建的test.txt文件，bash中已经提示了将文件add到暂存区。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020030119301745.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hobF9qYW1lcw==,size_16,color_FFFFFF,t_70)

## 三、提交文件

- 将文件添加到暂存区

```bash
git add .
1
```

> 这里的 . 表示所有文件，也可以添加单独的文件，不清楚的可以输入git add --help查看

- 提交暂存区的文件

提交前查看状态是怎样的，再次输入git status查看，一般都要随时看一下文件状态是怎样的。

```bash
git commit -m '提交test文件'
1
```

> 这时只是将文件提交到了本地仓库，并没有同步到远端。

## 四、 添加远端仓库

```bash
git remote add origin 你的远端厂库地址
1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200301193932484.png)

## 五、同步

```bash
git push
1
```

由于是第一次提交到远端，本地并还没有master分支，这时候直接使用–set-upstream进行同步。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200301194040537.png)

```bash
git push --set-upstream origin master
1
```

到这里整个初始化项目就与远端同步了，在实际开发中仅仅这点git知识是完全不够的，但是这也是常用的，
有需要后期可以分享其他知识，例如分支、标签、Flow、回滚等等
