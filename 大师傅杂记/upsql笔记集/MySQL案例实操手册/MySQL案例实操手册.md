## MySQL案例实操手册



#### 1.建库

```sql
--创建数据库
create schema [数据库名称] default character set utf8 collate utf8_general_ci;
例如：
create schema dsf_onldb default character set utf8 collate utf8_general_ci;
```

#### 2.建用户

```sql
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
```

#### 3.建表

```sql
--学生表
CREATE TABLE tbl_student(
s_id VARCHAR(20),
s_name VARCHAR(20) NOT NULL DEFAULT '',
s_birth VARCHAR(20) NOT NULL DEFAULT '',
s_sex VARCHAR(10) NOT NULL DEFAULT '',
PRIMARY KEY(s_id)
);

--课程表
CREATE TABLE tbl_course(
c_id VARCHAR(20),
c_name VARCHAR(20) NOT NULL DEFAULT '',
t_id VARCHAR(20) NOT NULL,
PRIMARY KEY(c_id)
);

--教师表
CREATE TABLE tbl_teacher(
t_id VARCHAR(20),
t_name VARCHAR(20) NOT NULL DEFAULT '',
PRIMARY KEY(t_id)
);

--成绩表
CREATE TABLE tbl_score(
s_id VARCHAR(20),
c_id VARCHAR(20),
s_score INT(3),
PRIMARY KEY(s_id,c_id)
);
```

#### 4.导数据

```sql
--插入学生表测试数据
insert into tbl_student values('01' , '赵雷' , '1990-01-01' , '男');
insert into tbl_student values('02' , '钱电' , '1990-12-21' , '男');
insert into tbl_student values('03' , '孙风' , '1990-05-20' , '男');
insert into tbl_student values('04' , '李云' , '1990-08-06' , '男');
insert into tbl_student values('05' , '周梅' , '1991-12-01' , '女');
insert into tbl_student values('06' , '吴兰' , '1992-03-01' , '女');
insert into tbl_student values('07' , '郑竹' , '1989-07-01' , '女');
insert into tbl_student values('08' , '王菊' , '1990-01-20' , '女');

--课程表测试数据
insert into tbl_course values('01' , '语文' , '02');
insert into tbl_course values('02' , '数学' , '01');
insert into tbl_course values('03' , '英语' , '03');

--教师表测试数据
insert into tbl_teacher values('01' , '张三');
insert into tbl_teacher values('02' , '李四');
insert into tbl_teacher values('03' , '王五');

--成绩表测试数据
insert into tbl_score values('01' , '01' , 80);
insert into tbl_score values('01' , '02' , 90);
insert into tbl_score values('01' , '03' , 99);
insert into tbl_score values('02' , '01' , 70);
insert into tbl_score values('02' , '02' , 60);
insert into tbl_score values('02' , '03' , 80);
insert into tbl_score values('03' , '01' , 80);
insert into tbl_score values('03' , '02' , 80);
insert into tbl_score values('03' , '03' , 80);
insert into tbl_score values('04' , '01' , 50);
insert into tbl_score values('04' , '02' , 30);
insert into tbl_score values('04' , '03' , 20);
insert into tbl_score values('05' , '01' , 76);
insert into tbl_score values('05' , '02' , 87);
insert into tbl_score values('06' , '01' , 31);
insert into tbl_score values('06' , '03' , 34);
insert into tbl_score values('07' , '02' , 89);
insert into tbl_score values('07' , '03' , 98);
```

