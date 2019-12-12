---
title: "Mysql"
date: 2019-12-10T15:20:56+08:00
draft: true
author:
  name: "Jane"
comments: true
description: ""
keywords:
images:
tags:
  - untagged
---

#### MySQL数据库####

MySQL 是一个关系型数据库管理系统，由瑞典 MySQL AB 公司开发，目前属于 Oracle 公司。MySQL 是一种关联数据库管理系统，关联数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。

#### MySQL安装####


#### MySQL连接####

使用命令行连接

```mysql
[root@host]# mysql -u root -p
Enter password:******
```

#### 创建数据库####

```mysql
CREATE DATABASE 数据库名;
```

#### 删除数据库####

```mysql
drop database <数据库名>;
```

#### 选择数据库####

在连接到 MySQL 数据库后，可能有多个可以操作的数据库，所以需要选择你要操作的数据库。

```mysql
[root@host]# mysql -u root -p
Enter password:******
mysql> use RUNOOB;
Database changed
mysql>
```

#### 数据类型####

MySQL中定义数据字段的类型对数据库的优化是非常重要的。

MySQL支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型。

- 数值类型

严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)

| 类型 | 大小 | 范围（有符号）|	范围（无符号）|	用途 |
| :--: | :--: | :----: | :----: | :------: |
| TINYINT	| 1 字节 |	(-128，127) |	(0，255) |	小整数值 |
| SMALLINT |	2 字节 |	(-32 768，32 767) |	(0，65 535) |	大整数值 |
| MEDIUMINT	| 3 字节 |	(-8 388 608，8 388 607)	| (0，16 777 215)	| 大整数值 |
| INT或INTEGER |	4 字节 |	(-2 147 483 648，2 147 483 647)	| (0，4 294 967 295) |	大整数值 |
| BIGINT |	8 字节 |	(-9,223,372,036,854,775,808，9 223 372 036 854 775 807) |	(0，18 446 744 073 709 551 615) |	极大整数值 |
| FLOAT | 4 字节 |	(-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) |	0，(1.175 494 351 E-38，3.402 823 466 E+38)	| 单精度浮点数值 |
| DOUBLE	| 8 字节 |	(-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) |	0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308)	| 双精度浮点数值 |
| DECIMAL |	对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 |	依赖于M和D的值 |	依赖于M和D的值 |	小数值 |

- 日期类型

表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。

每个时间类型有一个有效值范围和一个"零"值，当指定不合法的MySQL不能表示的值时使用"零"值。

TIMESTAMP类型有专有的自动更新特性

| 类型|	大小(字节) |	范围 |	格式 |	用途 |
| ---- | ---- | ---- | ---- | ---- |
| DATE |	3 |	1000-01-01/9999-12-31	| YYYY-MM-DD |	日期值 |
| TIME |	3 | '-838:59:59'/'838:59:59' |	HH:MM:SS |	时间值或持续时间 |
| YEAR |	1	| 1901/2155 |	YYYY |	年份值 |
| DATETIME |	8	| 1000-01-01 00:00:00/9999-12-31 23:59:59	| YYYY-MM-DD HH:MM:SS	| 混合日期和时间值 |
| TIMESTAMP |	4	| 1970-01-01 00:00:00/2038 结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYYMMDD HHMMSS | 混合日期和时间值，时间戳 |


- 字符串类型

| 类型 |	大小 |	用途 |
| ---- | ---- | ---- |
| CHAR |	0-255字节	| 定长字符串 |
| VARCHAR	| 0-65535 字节 |	变长字符串 |
| TINYBLOB |	0-255字节	| 不超过 255 个字符的二进制字符串 |
| TINYTEXT |	0-255字节	| 短文本字符串 |
| BLOB |	0-65 535字节 |	二进制形式的长文本数据 |
| TEXT	| 0-65 535字节 |	长文本数据 |
| MEDIUMBLOB	| 0-16 777 215字节 |	二进制形式的中等长度文本数据 |
| MEDIUMTEXT |	0-16 777 215字节 |	中等长度文本数据 |
| LONGBLOB	| 0-4 294 967 295字节	| 二进制形式的极大文本数据 |
| LONGTEXT	| 0-4 294 967 295字节 |	极大文本数据 |


#### 创建数据表####

语法：

```mysql
CREATE TABLE table_name (column_name column_type);
```
例子：

```mysql

CREATE TABLE IF NOT EXISTS `test_tbl`(
   `test_id` INT UNSIGNED AUTO_INCREMENT,
   `test_title` VARCHAR(100) NOT NULL,
   `test_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
   PRIMARY KEY ( `test_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

```

#### 删除数据表####

```mysql
DROP TABLE table_name ;
```


