## MySQL初始化实战操作汇总



#### 1.数据库基本信息操作



1.什么是SQL？
	Structured Query Language：结构化查询语言
	其实就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方，称为“方言”。
	
2.SQL通用语法
	1. SQL 语句可以单行或多行书写，以分号结尾。
	2. 可使用空格和缩进来增强语句的可读性。
	3. MySQL 数据库的 SQL 语句不区分大小写，关键字建议使用大写。
	4. 3 种注释
		* 单行注释: -- 注释内容 或 # 注释内容(mysql 特有) 
		* 多行注释: /* 注释 */

3.SQL分类

1) DDL(Data Definition Language)数据定义语言
    用来定义数据库对象：数据库，表，列等。关键字：create, drop,alter 等
2) DML(Data Manipulation Language)数据操作语言
    用来对数据库中表的数据进行增删改。关键字：insert, delete, update 等
3) DQL(Data Query Language)数据查询语言
    用来查询数据库中表的记录(数据)。关键字：select, where 等
4) DCL(Data Control Language)数据控制语言(了解)
    用来定义数据库的访问权限和安全级别，及创建用户。关键字：GRANT， REVOKE 等



##### 1.1 查看数据库版本

###### 1.1.1 mysql --version

```shell
dsfu@dsfudeMacBook-Pro document % mysql --version
mysql  Ver 8.0.32 for macos13 on x86_64 (MySQL Community Server - GPL)
```

###### 1.1.2 select version();

```sql
mysql> select version();
+---------------+
| version()     |
+---------------+
| 8.0.25-221000 |
+---------------+
1 row in set (0.05 sec)
```



##### 1.2 数据库登录

```shell
dsfu@dsfudeMacBook-Pro Certificate Download % mysql -h xxx.xxx.xxx.xxx -P 3306 -u root -p --ssl-ca=ca.pem
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 68310
Server version: 8.0.25-221000 MySQL Community Server - (GPL)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

###### 1.2.1 命令

```sql
mysql -u (用户名) -h (mysql服务所在地址) -u (用户名) -P (可选默认3306 指定端口号) -p

mysql -u root -h 127.0.0.1 -P3306 -u root -p
```



##### 1.3 数据库建库和授权

```sql
show databases;                 --显示数据库列表                
use 数据库名称;                  --使用指定数据库
show tables;                    --显示当前数据库下的列表
show create table 表名\G;        --其中”\G”是格式化输出结果，下同。
 
--创建数据库
create schema [数据库名称] default character set utf8 collate utf8_general_ci;
例如：
create schema dsf_onldb default character set utf8 collate utf8_general_ci;

--创建用户
## 密码8位以上，包括：大写字母、小写字母、数字、特殊字符
## %：匹配所有主机，该地方还可以设置成‘localhost’，代表只能本地访问，例如root账户默认为‘localhost‘
create user '[用户名称]'@'%' identified by '[用户密码]';
例如：
create user 'dsfonlad'@'%' identified by 'xxxxxxx';

--用户授权数据库
## *代表整个数据库
grant select,insert,update,delete,create on [数据库名称].* to [用户名称];
例如：
grant select,insert,update,delete,create on dsf_onldb.* to dsfonlap; 

--权限更大赋值：
grant all privileges on 库名.表名 to '用户名'@'IP地址' identified by '密码' with grant option;
例如：
grant all privileges on dsf_onldb.* to dsfonlad; 
 
--立即启用修改
flush  privileges;

--取消用户所有数据库（表）的所有权限
revoke all on *.* from tester;

--删除用户
delete from mysql.user where user='tester';

--删除数据库
drop database [schema名称|数据库名称];
```



1.4 常用操作数据库的指令



<table>
  <tr>
   <th>sss</th>
   <th>sss</th>
  </tr>
  <tr>
    <td>sss</td>
    <td>sss</td>
  </tr>
</table>




<div style="width:80px">


| <span style="display:inline-block;width:80px">类型</span> | <span style="display:inline-block;width:80px">命令</span> |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
|         试试啊飒飒c.     Sass信息行下下下下下下下         |                         信息行 下                         |
|           <div style="width: 150pt"> dd </div>            |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |
|                                                           |                                                           |

</div>
