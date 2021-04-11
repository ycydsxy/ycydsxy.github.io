---
title: MySQL NULL 值的运算问题
date: 2020-11-30 21:24:40
tags: 
- MySQL
- Null
- 被动离职警告
categories: 数据库
---

我在使用 MySQL 时遇到了一个关于 Null 值问题，起初让我比较疑惑。比如，我需要在表 `table` 中筛选出 `id=1` 且 ` b`  列的值不等于 b 的所有记录的数量，很容易写出这种 SQL：

```sql
SELECT count(*) FROM `table` WHERE id = 1 AND NOT (b = 'b');
```

或者

```sql
SELECT count(*) FROM `table` WHERE id = 1 AND b <> 'b';
```

但是很遗憾，这个写法是错误的，实际得到的结果数量是小于我们预期的数量的

<!-- more -->

# 问题所在

最终执行的过程中，以上的 SQL 会忽略 `b` 列为 `NULL` 的记录，即上述 SQL 和下面能够满足我们需求的 SQL 其实不是等价的

```sql
SELECT count(*) FROM `table` WHERE id = 1 AND (NOT (b = 'b' AND b IS NOT NULL));
```

从逻辑上说， `b == 'b'` 的「非」表述就是 `!(b == 'b')` ，这没毛病，这个问题的关键就是在于 MySQL 对于 `NULL` 值的处理上

 `NULL` 是 MySQL 中的一种比较特殊的值，我们知道它表示的是一种未定义的空状态，其有一些特殊的特性：

* 占用空间：NULL columns require additional space in the row to record whether their values are NULL.
* 需要使用 `IS NULL` 或者 `IS NOT NULL` 来判断，而不能使用平常的算术运算符，如 `=`、`<`、`<>` 等
* 排序时正序排在第一个，倒序最后一个
* 聚合函数如 `count`、`min`、`sum` 均会忽略（ `count(*)` 除外）
* `distinct`、`group` 时认为所有 `NULL` 值均一样
* 对时间戳类型的列插入 `NULL` 值时，插入的是当前时间；对自增整型或者浮点型列插入 `NULL` 值时，插入的是下一个数
* ......

为什么不能使用算数运算符来判断 `NULL` 值呢？简单来说，就是关于 `NULL` 值的所有**算数运算**操作，结果都是 `NULL`。比如：

| 表达式     | 值   |
| ---------- | ---- |
| 1 = NULL   | NULL |
| 1 <> NULL  | NULL |
| 1 < NULL   | NULL |
| 1 > NULL   | NULL |
| 1 xxx NULL | NULL |

在布尔运算中，`NULL` 值的表现为：

| 表达式         | 值   |
| -------------- | ---- |
| true AND NULL  | NULL |
| true OR NULL   | 1    |
| false AND NULL | 0    |
| false OR NULL  | NULL |
| !NULL          | NULL |

而 MySQL 中，0 或者 NULL 值被看作是 **false**，所以最开始的例子中，如果 `b` 列是 `NULL` 值，则 where 条件的演变路径为：

```sql
id = 1 AND NOT (NULL = 'b') /*-->*/
id = 1 AND NOT (NULL) /*-->*/
id = 1 AND NULL /*-->*/
NULL /*-->*/
false
```

所以，该记录是不会被筛选出来的。

# 总结

* MySQL中 `NULL` 值的所有算术运算结果都是 NULL
* MySQL中 `NULL` 值的布尔运算结果大多数是 NULL
* 在含有 `NULL` 值的列上进行逻辑处理需要小心边界

# 参考资料

* [MySQL 5.7 的官方文档 - Working with NULL Values](https://dev.mysql.com/doc/refman/5.7/en/working-with-null.html)
* [MySQL 5.7 的官方文档 - Problems with NULL Values](https://dev.mysql.com/doc/refman/5.7/en/problems-with-null.html)



