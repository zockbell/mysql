# MySQL数据库探索

## 数据库概念

>  按照数据结构来组织、存储和管理数据的仓库。

## MySQL优点

* 采用结构化查询语言SQL访问数据库
* 支持Linux、Mac os、Windows等多种操作系统
* 为多种编程语言提供API,如C、Java、PHP……
* 开源的，无需支付额外的费用
* 提供用于管理、检查、优化数据库操作的管理工具
* ……

## MySQL可视化管理工具

* Windows: Navicat Premium \ PHPMyAdmin \ MySQL_Front
* Mac: Navicat Premium \ PHPMyAdmin \ Sequel Pro

## 连接MySQL数据库

* Host：127.0.0.1 或者 localhost
* Username：root
* Password：对应的root用户的密码
* Port：3306

## Table表

| username | content                                    |
| -------- | ------------------------------------------ |
| zock     | 希望肺炎疫情尽快结束！                     |
| 张三     | 詹皇浓眉合砍61分湖人险胜凯尔特人           |
| 李四     | 今天裁判真的没有帮湖人，浓眉有很多篮下进攻 |
| vue      | 布朗没吃假动作，，只后仰跳投没法防         |
| 腾讯体育 | 25日凌晨2点视频直播科比追思会              |



## MySQL数据类型作用

* 限制可在存储在列中的数据
* 更有效地存储数据
* 变换排序顺序
  * 字符串排序：1， 10， 2
  * 数据排序： 1， 2， 10

## 字段类型type - 整数

| 数据类型  | 数值范围               |
| --------- | ---------------------- |
| tinyint   | -128~127               |
| smallint  | -32768~32767           |
| mediumint | -8388608~8388607       |
| int       | -1247482648~2147483647 |
| bigint    | +-9.22*10的18次方      |

*  Length（长度/值）
   * 与整型的数据类型搭配，表示最大显示宽度。
*  default默认值
   * 必须是常量
*  unsigned
   * 定义无符号的数值，对应的取值范围翻倍

## 字段类型type - 字符串

| 数据类型   | 含义                  |
| ---------- | --------------------- |
| char       | 最多255个字符         |
| varchar    | 最多65532个字符       |
| tinytext   | 最多255个字符         |
| text       | 最多65535个字符       |
| mediumtext | 最多2的24次方-1个字符 |
| Longtext   | 最多2的32次方-1个字符 |



## 字段类型type - 日期/时间

| 数据类型  | 含义                                |
| --------- | ----------------------------------- |
| date      | 日期，格式：YYYY-MM-DD              |
| time      | 时间，格式：HH:MM:SS                |
| datetime  | 日期时间，格式：YYYY-MM-DD HH:MM:SS |
| timestamp | 功能和datetime相同（但范围较小）    |
| year      | 年份，格式：YYYY                    |

* binary
  * 只用于char和varchar值。当字段指定了该属性时，将以区分大小写的方式排序。
* NULL
  * 指定null属性时，该列可以保持为空。
* NOT NULL
  * 如果将一个列定义为not null,将不允许向该列插入null值。

![](https://github.com/zockbell/mysql/blob/master/img/1.png)

## 数据库设计范式

* 第一范式 无重复的列
* 第二范式 属性完全依赖于主键
* 第三范式 属性不能依赖于主属性

### 第一范式（1NF）

数据库表的每一列都是不可分割的基本数据项，同一列中不能有多个值

### 理解第一范式

* 每一次属性都是不可再分的，确保每一列的原子性。
* 两列的属性相近或相似或一样，尽量合并属性一样的列，确保不产生冗余数据。

#### 理解第一范式--考勤表

需求是：想做一张所有学生每天的考勤表。

1. 不能像下图中交叉的存储数据

![](https://github.com/zockbell/mysql/blob/master/img/2.png)

2. 不能像下图这样每天都建一张表

![](https://github.com/zockbell/mysql/blob/master/img/3.png)

3. 也不能像这图这样每个字段的含义都是相同的

![](https://github.com/zockbell/mysql/blob/master/img/4.png)

4. 正确的做法如下图：

![](https://github.com/zockbell/mysql/blob/master/img/5.png)

## 索引

* 普通索引	index
* 唯一索引    unique
* 主键            primary key
* 全文索引    fulltext
* 空间索引    spatial

### 索引优点

* 大大加快数据查询速度
* 通过创建唯一索引，保证数据库表每行数据的唯一性

### 索引缺点

* 维护索引需要耗费数据资源
* 占用磁盘空间
* 影响对表的数据进行增删改的速度

#### 索引应用

* INDEX索引        性能优化
* UNIQUE索引     避免数据出现重复
* PRIMARY索引    标识行

### 主健

* 值唯一
* 不允许NULL值
* 可以在创建表时定义，也可以在创建表之后定义。

### auto_increment（自动递增）

* 自动生成整数值
* 新值为上一次插入的值 +1
* 只适用于整数列
* 必须有唯一索引 
* 必须具备NOT NULL属性

如下图中红框为主键显示，蓝框为audo_increment选择

![](https://github.com/zockbell/mysql/blob/master/img/6.png)

## 第二范式（2NF）

* 一个表必须有一个主键
* 且没有包含在主键中的列必须完全依赖于主键，而不能只依赖于主键的一部分

### 理解第二范式 -- 购物车

下图中单位和数量并不依赖于用户ID，而是依赖于商品ID，帮设计有缺陷

![](https://github.com/zockbell/mysql/blob/master/img/7.png)

应该像下图这样设计：

![](https://github.com/zockbell/mysql/blob/master/img/8.png)

## 第三范式（3NF）

* 非主键列必须直接依赖于主键，不能存在传递依赖。

### 第三范式 -- 中奖信息表

下图中主键为用户ID，中奖金额并不依赖于用户ID，而是依赖于中奖等级，所以设计不对，应该消除这样的传递依赖

![](https://github.com/zockbell/mysql/blob/master/img/9.png)

应该像下图这样设计两张表：

![](https://github.com/zockbell/mysql/blob/master/img/10.png)

## 实践--创建三张表

* user表：用户名、密码、是否是管理员
* news表：新闻标题、新闻内容、作者、新闻时间、是否上线
* comment表：评论人、评论内容、评论时间、评论源

要求如下：

* 用户名：长度不超过20个字符 
* 密码：长度不超过20个字符 
* 新闻标题：长度不超过30个字符 
* 新闻内容：长度不超过5000个字符 
* 评论内容：长度不超过300个字符 

![](https://github.com/zockbell/mysql/blob/master/img/11.png)

![](https://github.com/zockbell/mysql/blob/master/img/12.png)

![](https://github.com/zockbell/mysql/blob/master/img/13.png)

## SQL语句

> Structured Query Language结构化查询语句，一种专门用来与数据库通信的语言。

* 几乎所有重要的DBMS（管理系统）谁都支持SQL
* 简单易学
* 可以进行非常复杂和高级的数据库操作

### 插入insert -- 插入完整行

```insert into 表名 values(值1, 值2, 值3, ...);```

* 插入的值的顺序必须和表中所有列顺序一一对应
* 英文括号、英文引号、英语逗号
* SQL语句不区分大小写
* 多条SQL需要用分号分隔，单条SQL语句无需分号结束
* 不推荐，推荐插入行的一部分

![](https://github.com/zockbell/mysql/blob/master/img/14.png)

插入成功：

![](https://github.com/zockbell/mysql/blob/master/img/15.png)

### 插入insert -- 插入行的一部分

```insert into 表名(列1, 列2, 表3, ...) values(值1, 值2, 值3,...);```

* 可以只给某些列提供值，某些列不提供值
* 必须要给不允许NULL值且没有默认值的列提供值，否则插入不成功

![](https://github.com/zockbell/mysql/blob/master/img/16.png)

没有指定的字段会用默认值填充

![](https://github.com/zockbell/mysql/blob/master/img/17.png)

### 插入insert -- 插入多行

```insert into 表名(列1, 列2, 列3, ...) values (值1,值2,值3,...), (值1,值2,值3,...),...;```

* 可以提高数据库处理的性能

---

## 检索查询select

* select 列名1 from 表名;
* select 列名1, 列名2, 列名3,... from 表名;
* select *1 from 表名;

## 过滤数据 -- where

* 搜索条件，where子句，放在from表名后面。

### where子句操作符

| 操作符  | 说明               |
| ------- | ------------------ |
| =       | 等于               |
| <>      | 不等于             |
| !=      | 不等于             |
| <       | 小于               |
| <=      | 小于等于           |
| >       | 大于               |
| >=      | 大于等于           |
| between | 在指定的两个值之间 |

例：

```SELECT * FROM `user` WHERE LEVEL BETWEEN 50 AND 100;```

![](https://github.com/zockbell/mysql/blob/master/img/18.png)

![](https://github.com/zockbell/mysql/blob/master/img/19.png)

### 空值检查

* is null
* 一个列不包含值时，称其包含空值NULL
* NULL与字段包含0，空字符串或仅仅包含空格不同

例：

```SELECT * FROM `user` WHERE LEVEL is NULL;```

### 组合where子名

| 操作符 | 说明             |
| ------ | ---------------- |
| AND    | 与               |
| OR     | 或               |
| IN     | 匹配值，与OR相当 |
| NOT    | 非               |

例：

```SELECT * FROM `user` WHERE username = 'zock' or username = 'admin'; ```

> 注：AND的优先级高于OR，下句会先查询and语句，再查询or语句

```SELECT * FROM `user` WHERE username = 'zock' or username = 'admin' AND is_admin = 1```

> 如果想先查询or语句，可以用括号先把前半句包含起来

```SELECT * FROM `user` WHERE (username = 'zock' or username = 'admin') AND is_admin = 1```

**in 语句**

```mysql
SELECT * FROM `user` WHERE username in ('zock','admin');
```

![](https://github.com/zockbell/mysql/blob/master/img/20.png)

> 说明：IN操作符比OR操作符执行速度更快，如果能用IN，尽量不用OR

**NOT 操作符**

```mysql
SELECT * FROM `user` WHERE username not in ('zock','admin');
```

![](https://github.com/zockbell/mysql/blob/master/img/21.png)

### like -- 不确定值的匹配（模糊匹配）

| 通配符 | 说明                   |
| ------ | ---------------------- |
| %      | 匹配任意字符、任意次数 |
| _      | 总是匹配一个字符       |

例：下句将所以包含zhang的用户名检索出来

```mysql
SELECT * FROM `user` WHERE username LIKE '%zhang%'
```

![](https://github.com/zockbell/mysql/blob/master/img/22.png)

---

## 更新数据 -- update特定行

```update 表名 set 列名1 = 值1, 列名2 = 值2, ... where 子句```

* 如果不是where 子句，将会修改表中所有行

例：下句将uid = 7 的用户名修改为 ```2020```

```mysql
UPDATE `user` SET username = '2020' where uid = 7;
```

![](https://github.com/zockbell/mysql/blob/master/img/23.png)

---

## 删除数据 -- delete特定行

```delete from 表名 where 子句```

* 如果不写where子句，将会删除表中所有行

例：下句执行，会删除uid = 7的记录

```mysql
DELETE FROM `user` where uid = 7;
```

## 排序 -- order by

* 默认升序（ASC）排序
* 降序排序 DESC
* order by 列名1；
* order by 列名1, 列名2；
* order by 列名1 DESC, 列名2；
* order by 列名1 DESC, 列名2 DESC；
* 如果有where子名，放在where子名之后

例：下句将user表中用户level降序查询出来

```mysql
SELECT * FROM `user` ORDER BY level DESC;
```

![](https://github.com/zockbell/mysql/blob/master/img/24.png)

例：多个列名排序

```mysql
SELECT * FROM `user` ORDER BY is_admin DESC, LEVEL DESC;
```

![](https://github.com/zockbell/mysql/blob/master/img/25.png)

---

## 限定结果 -- limit （常见于分页）

* limit 5;
* 第一行为0而不是1
* limit 1, 1;
* 放在where子句、order by 子句之后

例：下句查询等级最高的前三名用户

```mysql
SELECT * FROM `user` ORDER BY LEVEL DESC LIMIT 3;
```

![](https://github.com/zockbell/mysql/blob/master/img/26.png)

---

## 计算字段 

| 操作符 | 说明 |
| ------ | ---- |
| +      | 加法 |
| -      | 减法 |
| *      | 乘法 |
| /      | 除法 |

例：下句检索会新加一列（price*quantiey）

```mysql
SELECT *, price*quantiey FROM `order`;
```

![](https://github.com/zockbell/mysql/blob/master/img/27.png)

## 使用别名 -- as

* 别名是一个字段或值的替换名
* 别名使用as关键字赋予

```mysql
SELECT *, price*quantiey as totalfee FROM `order`;
```

![](https://github.com/zockbell/mysql/blob/master/img/28.png)

## 汇总数据 -- 聚集函数

| 函数    | 说明             |
| ------- | ---------------- |
| Avg()   | 返回某列的平均值 |
| Count() | 返回某列的行数   |
| Max()   | 返回某列的最大值 |
| Min()   | 返回某列的最小值 |
| Sum()   | 反回某列值之后   |

例：下句中将返回user表中level字段的平均值

```mysql
SELECT AVG(level)	FROM `USER`;
```

![](https://github.com/zockbell/mysql/blob/master/img/29.png)

---

## 分组汇总 -- gruop by

* 批示mysql分组数据，然后对每个组进行聚集
* 必须出现在where子句后，order by 子句前
* 除聚集计算语句外，select语句中的列都必须在group by子句给出

例：下句查询每日的签到分组

```mysql
SELECT date, COUNT(*) FROM `ATTENCE` WHERE STATUS = 1 GROUP BY date
```

![](https://github.com/zockbell/mysql/blob/master/img/30.png)

---

## 分组数据过滤 -- having 

* Where 过滤指定的是行而不是分组
* having支持所有where操作符号
* 必须出现在group by之后

```mysql
SELECT date, COUNT(*) as totalcout FROM `ATTENCE` WHERE STATUS = 1 GROUP BY date having count(*) < 2 order by date desc;
```

## select 子句顺序

| 子名     | 说明             | 是否必须使用           |
| -------- | ---------------- | ---------------------- |
| select   | 返回数据         | 是                     |
| from     | 从中检索数据的表 | 从表中选择数据时使用   |
| where    | 行级过滤         | 否                     |
| group by | 分组             | 仅在按组计算聚集时使用 |
| having   | 组级过滤         | 否                     |
| order by | 排序             | 否                     |
| limit    | 限制检索的行     | 否                     |

## 连表查询 -- 联结

* 在一条select语句中关联表，称为联结
* 联结多个表返回一组输出
* 不要忘记where子句

```mysql
SELECT * FROM `news`, `user` where news.admin_id = user.uid;
```

![](https://github.com/zockbell/mysql/blob/master/img/31.png)

例：如果只想显示news的所有信息，但是只显示user的username信息，可以这样执行：

```mysql
SELECT news.*,user.username FROM `news`, `user` where news.admin_id = user.uid;
```

![](https://github.com/zockbell/mysql/blob/master/img/32.png)

## join

* 如果表中有至少一个匹配，则返回行
* 联结条件用特定的on子句而不是where子名
* Inner join 和 join 是相同的

```mysql
SELECT news.*, user.username FROM `news` join `user` on news.admin_id = user.uid
```

---

## MySQL、MySQLi和PDO

* mysql扩展提供来一个面向过程的接口
* mysqli扩展提供了面向对象接口
* pdo数据对象是一个数据库抽象层规范，提供了统一的API接口

> mysql介绍到此，谢谢观看！

