---
title: oracle数据库学习笔记
date: 2024-07-16 17:02:17
tags: oracle
---

# oracle数据库学习笔记

## 相关sql语句

1. **列出所有数据库**: 在Oracle中，通常使用实例来代表一个数据库。要查看连接到的数据库实例的信息，可以使用以下命令：

	```sql
	SELECT INSTANCE_NAME FROM V$INSTANCE;
	```

2. **列出所有表空间**: 表空间是数据库中存储数据的逻辑单元。要列出所有的表空间，可以使用：

	```sql
	SELECT TABLESPACE_NAME FROM DBA_TABLESPACES;
	```

3. **列出特定用户的所有表**: 要列出特定用户（例如用户 `ZWXBDN1`）的所有表，您可以使用：

	```sql
	SELECT TABLE_NAME FROM ALL_TABLES WHERE OWNER = 'ZWXBDN1';
	```

4. **列出所有表的列信息**: 要获取所有表的列信息，可以使用：

	```sql
	SELECT TABLE_NAME, COLUMN_NAME, DATA_TYPE, DATA_LENGTH 
	FROM USER_TAB_COLUMNS;
	```

5. **查看表的记录**: 要查看某个特定表的记录，您可以使用`SELECT *`语句，例如：

	```sql
	SELECT * FROM ZWXBDN1.your_table_name;
	```

	请将 `your_table_name` 替换为您想要查看的表名。

6. **查看表的前几行记录**: 如果您只想查看表的前几行记录，可以使用`ROWNUM`限制结果集，例如：

	```sql
	SELECT * FROM ZWXBDN1.your_table_name WHERE ROWNUM <= 10;
	```

7. **查看数据库的统计信息**: 要查看数据库的统计信息和其他信息，可以使用：

	```sql
	SELECT * FROM V$DATABASE;
	```

8. **查看数据库的版本信息**: 要查看数据库的版本信息，可以使用：

	```sql
	SELECT * FROM V$VERSION;
	```

请注意，您需要具有足够的权限来执行上述查询。如果您没有权限访问`DBA_`视图，您可能需要使用以您的用户名为前缀的视图，如`USER_`或`ALL_`视图。

<!-- more -->





1. **查询所有表名**： 首先，查询出该用户所有的表名：

	```sql
	SELECT table_name FROM all_tables WHERE owner = 'ZWXBDN1';
	```

要查询用户 `ZWXBDN1` 的所有表分别属于哪个表空间，您可以使用以下SQL查询：

```sql
SELECT table_name, tablespace_name 
FROM all_tables 
WHERE owner = 'ZWXBDN1';
```

这个查询会列出用户 `ZWXBDN1` 拥有的所有表及其对应的表空间名称。`all_tables` 视图包含了所有用户的表的信息，其中 `table_name` 是表的名称，`tablespace_name` 是表所属的表空间名称。

1. **列出所有表**： 首先，获取用户 `ZWXBDN1` 下所有表的列表：

	```sql
	SELECT table_name FROM all_tables WHERE owner = 'ZWXBDN1' ORDER BY table_name;
	```



1. **准备删除语句**： 对于列表中的每个表，准备一个 `DROP TABLE` 语句。例如，如果要删除名为 `BASE_CAR` 的表，使用以下语句：

	```sql
	DROP TABLE ZWXBDN1.BASE_CAR CASCADE CONSTRAINTS;
	```

	`CASCADE CONSTRAINTS` 子句用于自动删除表上定义的所有约束（如外键约束）。


在Oracle数据库中，要列出所有表空间，您可以使用以下SQL查询：

```sql
SELECT tablespace_name FROM dba_tablespaces;
```

这个查询会返回数据库中所有表空间的名称。`dba_tablespaces` 是一个包含所有表空间信息的数据字典视图，只有数据库管理员或具有适当权限的用户才能访问。



如果您是以普通用户身份连接到数据库，并且没有权限访问 `dba_tablespaces`，您可以尝试使用以下查询来查看您有权限访问的表空间列表：

```sql
SELECT DISTINCT tablespace_name FROM all_tables
WHERE owner = 'YOUR_USERNAME';
```



在Oracle数据库中，创建一个新的表空间涉及指定表空间的名称和相关属性。以下是一个基本的SQL命令，用于创建一个名为 `XMDJ` 的表空间：

```sql
CREATE TABLESPACE XMDJ
DATAFILE 'path_to_datafile.dbf' SIZE 100M
EXTENT MANAGEMENT LOCAL
UNIFORM SIZE 1M;
```



自动扩展表空间大小

```sql
alter database datafile 'D:\application\oracle\oradata\XMDJ.dbf' resize 1024M;
alter database datafile 'D:\application\oracle\oradata\XMDJ.dbf' autoextend on next 100m maxsize 10000m
```



## 有用（work)

1. **查询所有表名**： 首先，查询出该用户所有的表名：

	```sql
	SELECT table_name FROM all_tables WHERE owner = 'ZWXBDN1';
	```

要查询用户 `ZWXBDN1` 的所有表分别属于哪个表空间，您可以使用以下SQL查询：

```sql
SELECT table_name, tablespace_name 
FROM all_tables 
WHERE owner = 'ZWXBDN1';
```

这个查询会列出用户 `ZWXBDN1` 拥有的所有表及其对应的表空间名称。`all_tables` 视图包含了所有用户的表的信息，其中 `table_name` 是表的名称，`tablespace_name` 是表所属的表空间名称。

