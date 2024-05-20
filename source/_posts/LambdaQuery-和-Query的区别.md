---
title: LambdaQuery 和 Query的区别
date: 2024-04-25 16:02:44
tags: java
---

在 MyBatis-Plus 中，`LambdaQuery` 和 `Query` 是两种不同的查询包装器，它们提供了不同的查询构建方式：

1. **QueryWrapper**：
	- `QueryWrapper` 是 MyBatis-Plus 提供的一个通用查询包装器，它允许您以链式调用的方式构建复杂的查询条件。
	- 它不依赖于实体类的字段，而是使用字符串来指定字段名，这使得它在某些情况下更加灵活，但也增加了字段名拼写错误的风险。
2. **LambdaQueryWrapper**：
	- `LambdaQueryWrapper` 是 `QueryWrapper` 的一个特殊版本，它使用 Java 8 的 Lambda 表达式来引用实体类的字段。
	- 通过 Lambda 表达式，您可以安全地引用实体类中的字段，而不必担心字段名拼写错误，因为编译器会在编译时检查字段名。
	- `LambdaQueryWrapper` 提供了类型安全的查询构建方式，通常被认为是更现代和更安全的选择。

以下是两种查询包装器的使用示例：

<!-- more -->

使用 `QueryWrapper`：

```
QueryWrapper<ShortLinkGotoDO> queryWrapper = new QueryWrapper<>();
queryWrapper.eq("full_short_url", fullShortUrl);
```

使用 `LambdaQueryWrapper`：

```
LambdaQueryWrapper<ShortLinkGotoDO> lambdaQueryWrapper = new LambdaQueryWrapper<>();
lambdaQueryWrapper.eq(ShortLinkGotoDO::getFullShortUrl, fullShortUrl);
```

在 `LambdaQueryWrapper` 中，`ShortLinkGotoDO::getFullShortUrl` 是一个方法引用，它引用了 `ShortLinkGotoDO` 实体类中获取 `fullShortUrl` 字段的方法。这种方式可以避免字符串硬编码，减少拼写错误的可能性，并且使代码更加清晰。
