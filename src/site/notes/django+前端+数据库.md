---
{"dg-publish":true,"permalink":"/django+前端+数据库/"}
---

mysql

mysql

## 2. Mysql 安装

### 2.1 安装

mysql-5.7.44-winx64.zip是免安装版本，触压后放到硬盘里，不要有中文路径;

### 2.2 创建配置文件

新建my.ini文件和data文件夹放到软件目录下，ini文件内容如下:

```
[client]
# 设置mysql客户端默认字符集
default-character-set=utf8
 
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=C:\\MyApps\\mysql-5.7.44-winx64
# 设置 mysql数据库的数据的存放目录，MySQL 8+ 不需要以下配置，系统自己生成即可，否则有可能报错
# datadir=C:\\MyApps\\mysql-5.7.44-winx64\\data
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

### 2.3 输入初始化命令

`"C:\MyApps\mysql-5.7.44-winx64\bin\mysqld.exe" --initialize-insecure`

### 2.4 启动mysql

启动MySQL一般有两种方式:

- 临时启动(不建议)

> > > “C:\MyApps\mysql-5.7.44-winx64\bin\mysqld.exe”

- 制作成Windows服务，服务来进行关闭和开启，
    
    - 制作服务  
        “C:\MyApps\mysql-5.7.44-winx64\bin\mysqld.exe” --install mysql57
- 启动服务
    
- net start mysql57
    
- 停止服务
    
- net stop mysql57
    

### 2.5 连接测试

> > > “C:\MyApps\mysql-5.7.44-winx64\bin\mysql.exe” -h 127.0.0.1 -P 3306 -u root -p
> > > 
> > > > “C:\MyApps\mysql-5.7.44-winx64\bin\mysql.exe” -u root -p

如果你将C:\MyApps\mysql-5.7.44-winx64\bin\添加到了系统环境变量。

> > > mysql -u root-p

### 2.6 设置密码

set password = password(“root123”)

[MySQL 安装 | 菜鸟教程](https://www.runoob.com/mysql/mysql-install.html)

## 3. MySql 指令

查看已有的数据库(文件夹)

> show databases;  
> 创建数据库(文件夹)  
> create database数据库名字DEFAULT CHARSET utf8 COLLATE utf8_general_ci;  
> create database gx day14 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;  
> 删除数据库(文件夹)  
> drop database gx day14;  
> 进入数据库(进入文件夹)  
> use gx day14;  
> 查看文件夹下所有的数据表(文件)  
> show tables;

### 3.1 创建数据库

```sql
create database 数据库名字 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
create database lx_data DEFAULT CHARSET utf8
collate utf8_general_ci;
```

### 3.2进入数据库

```sql
use lx_data;
```

### 3.3查看数据库

```sql
show lx_data;
```

### 3.4创建表

```sql
create table tb1(
     id int,
     name varchar(16),
     age int
     )default charset=utf8;
```

```sql
create table tb1(
     id int,
     name varchar(16) not null, --不允许为空
     age int null, --允许为空（默认）
     )default charset=utf8;
```

```sql
create table tb1(
     id int,
     name varchar(16) not null, --不允许为空
     age int default 3, --插入数据时，age列的值默认为3
     )default charset=utf8;
```

```sql
create table tb1(
	id int primary key,  --主键（不允许为空，不允许重复）
	name varchar(16),
	age int 
	)default charset=utf8;
```

```sql
create table tb1(
	id int auto_increment primary key,  --内部维护，自增
	name varchar(16),
	age int 
	)default charset=utf8;
```

```sql
create table tb1(
	id int not null auto_increment primary key,   --不允许为空，自增，不能重复
	name varchar(16),
	age int 
	)default charset=utf8;
```

### 3.5删除表

```sql
drop table tb1;
```

### 3.6 常用数据类型

- tinyint  
    有符号，取值范围:-128~127(有正有负)  
    无符号，取值范围:0-255(只有正)【默认】

```sql
create table tb1(
     id int,not null auto_increment primary key, 
     age tinyint --有符号，取值范围:-128~127(有正有负)
     )default charset=utf8;
```

```sql
create table tb1(
     id int,not null auto_increment primary key, 
     age tinyint unsigned --无符号，取值范围:0-255(只有正)【默认】
     )default charset=utf8;
```

- int  
    int 表示有符号，取值范围:-2147483648~2147483647  
    int unsigned 表示无符号，取值范围:0~4294967295

-bigint  
有符号，取值范围:-9223372036854775808~9223372036854775807  
无符号，取值范围:0~18446744073709551615

### 练习题：

```sql
create table tb1(
	id bigint not null auto_increment primary key, 
	salary int,
	age tinyint
	)default charset=utf8;
```

### 3.7 插入数据

```
insert into tb2(salary,age) values(10000,18);
insert into tb2(salary,age) values(20000,18);
insert into tb2(salary,age) values(30000,18),(40000,18);
```

### 3.8查看表中的数据

```
select * from tb2;
```

-float  
-double  
-decimal  
准确的小数值，m是数字总个数(负号不算)，d是小数点后个数。 m最大值为65，d最大值为30。  
例如:

```sql
create table tb3(
	id bigint not null auto_increment primary key, 
	salary salary decimal(8,2) --所有数字是8位，小数点后是2位
	)default charset=utf8;

insert into tb3(salary)values(1.28);
insert into tb3(salary)values(5.289);
insert into tb3(salary)values(5.282);

select * from tb3;
```

### 3.9 字符串

-char(m) 速度快

```sql
定长字符串,m代表字符串的长度，最多可容纳255个字符。
char(11)，固定用11个字符串进行存储，哪怕真是没有11个字符，也会按照11存储。
create table tb4(
	id int not null primary key auto_increment,
	mobile char(11)
	)default charsetsutf8;
insert into tb4(mobile)values("151");
insert into tb4(mobile)values("15131255555"); --超出报错
```

-varchar(m) 节省空间

```sql
变长字符串，m代表字符的长度。最大65535字节/3 = 最大的m(中文)
varchar(11)，真实数据有多少长久按照多长存储。超过一样会报错

create table tb5(
	id int not null primary key auto_increment,
	mobile varchar(11)
	)default charset.utf8;
	
insert into tb5(mobile)values("151");
insert into tb5(mobile)values("15131255555");
```

-text

```sql
text数据类型用于保存变长的大字符串，可以组多到65535(2**16-1)个字符。
一般情况下，长文本会用text类型。例如:文章、新闻等。
create table tb5(
	id int not null primary key auto increment,
	title varchar(128),
	content text
)default charset=utf8;
```

-mediumtext  
A TEXT column with amaximum lengthof 16,777,215(2**24-1)characters.

-longtext  
A TEXT column with a maximum length of 4,294,967,295 0r 4GB  
(2**32-1)

-datetime  
YYYY-MM-DD HH:MM:SS(1000-01-0100:00:00/9999-12-3123:59:59)

-date  
YYYY-MM-DD(1000-01-01/9999-12-31)

## 练习题：用户表

```sql
create table tb7(
	id int not null primary key auto_increment,
	name varchar(64)not null,
	password char(64)not null,
	email varchar(64)not null,
	age tinyint,
	salary decimal(10,2),
	ctime datetime
)default charset=utf8;

insert into tb7(name,password,email,age,salary,ctime)values("武沛齐","123","xxelive.com",19,1000.20,“2011-11-11 11:11:10")
insert into tb7(name,password,email,age,salary,ctime)values("张电摩","123","xxelive.com",19,1000.20,"2011-11-11 11:11:10");
insert into tb7(name,password,email,age,salary,ctime) values("庞小青","123","xxelive.com",19,1000.20,"2011-11-11 11:11:10");
insert into tb7(name,password,email,age,salary,ctime) values("谢涛","123","xx@live.com",19,1000.20,"2011-11-11 11:11:10");
insert into tb7(name,password,email,age,salary,ctime) values("谢鹏","123","xx@live.com",19,1000.20,"2011-11-11 11:11:107);

select * from tb7;
```

MySQL还有很多其他的数据类型，例如:set、enum、TinyBlob、Blob、MediumBlob、LongBlob 等，详细见官方文档:[https://dev](https://dev/),mysqlcom/doc/refman/5,7/en/data-types.html

我们平时开发系统时，一般情况下:

- 创建数据库
- 创建表结构  
    都是需要提前通过上述命令创建。

### 3.10 数据行操作

1.新增数据  
insert into 表名(列名,列名) values(值,值);  
insert into 表名(列名,列名) values(值,值),(值,值)，(值,值)，(值,值);

2.删除数据

```sql
delete from 表名;  --删所有
delete from 表名 where 条件; --删范围
delete from tb7;
delete from tb7 where id=3; 
delete from tb7 where id =4 and name="谢涛”;
delete from tb7 where id =4 or name="谢涛”;
delete from tb7 where id>4;
delete from tb7 where id >= 4;
delete from tb7 where id != 4;
delete from tb7 where id in (1,5);
```

3.修改数据

```sql
update 表名set 列=值;
update 表名 set 列-值,列-值;
update 表名 sot 列=值 where 条件;
```

```sql
update tb7 set password "哈哈哈”;
update tb7 set email-"哈哈哈”where id>5;
update tb7 set age=age+10 where id >5;
```

4.查询数据

```sql
select * from表名称;
select 列名称，列名称 from 表名称;
select 列名称,列名称 from 表名称 where id >3;
```

```sql
select * from tb7;
select id,name from tb7;
select id,name from tb7 where id >10;
select id,name from tb7 where name="xx" and password="xx"
```

## 小结

我们平时开发系统时，一般情况下:

- 创建数据库
- 创建表结构  
    都是需要提前通过工具+命令创建。  
    但是，表中的数据一般情况下都是通过程序来实现增删改查。

## 4.案例:员工管理

- 使用MySQL内置工具(命令)
    - 创建数据库:unicom  
        数据一张表:admin

```sql
	表名:admin
	列:
			id，整型，自增，主键。
			username 字符串 不为空
			password 字符串 不为空
			mobile 字符串 不为空
```

- Python代码实现:
    - 添加用户
    - 删除用户。
    - 查看用户
    - 更新用户信息

### 4.1 创建表结构

```sql
create database unicom DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
use unicom;

create table admin(
	id int not null auto_increment primary key,
	username varchar(16) not null,
	password varchar(64) not null,
	mobile char(11) not null
)default charset=utf8;
```

### 4.2 Python操作MySQL

#### 4.2.1 创建数据

> 用Python代码连接MySQL并发送指令  
> pip install pymysql

```python
import pymysql
#1.连接MySQL
conn = pymysql.connect(host="127.0.0.1", port=3306, user='root', passwd="root123", charset='utf8’, db='ynicam')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
#2.发送指令
#cursor.execute("insert into admin(username,password,mobile)values('wwpeig','qwe123','15155555555')")

#2.发送指令(千万不要用字符串格式化去做SQL的拼接，安全隐患S0L注入)
#sql = "insert into admin(username,password,mobile) values(%s,%s,%s)'
#cursor.execute(sql,〔"韩超"，"qwe123"，"1999999999"])

sql = "insert into admin(username,password,mobile) values(%(n1)s,%(n2)s,%(n3)s)
cursor.execute(sql，{"n1":"集宁","n2":"qwe123","n3":{"1999999999"})

conn.commit()
#3.关闭
cursor.close()
conn.close()
```

```python
动态创建
import pymysqL
while True :
	user = input("用户名:”)
	if user.upper()== 'Q';
		break
	pwd = input("密码:”)
	mobile =input("手机号:”)
	#1.连接MySQL
	conn= pymysql.connect(host="127.0.0.1",port=3306,user='root', passwd="root123",charset='utf8',db='unicom') 
	cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
	#2.发送指令(***千万不要用字符串格式化去做S0L的拼接，安全隐惠SQL注入***)
	sql = "insert into admin(username,password,mobile) values(%s,%s,%s)
	cursor.execute(sql,[user,pwd, mobile])
	conn.commit()
	# 3.关闭
	cursor.close()
	conn.close()
```

#### 4.2.1 查询数据

```python
import pymysql
# 1.连接MySQL
conn =pymysql.connect(host="127.0.0.1",port=3306, user='root'passwd="rootl23"charset='utf8'，db='unicom')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

# 2.发送指令(***千万不要用字符串格式化去做SQL的拼接，安全隐患SQL注入***)
#cursor.execute("select *from admin where id > 2)
cursor.execute("select *from admin where id > %s",[2,])
#fetchall获取符合条件的所有数据，得到的是[字典,字典，]，没有数据就是空列表
data_list=cursor.fetchall()
for row dict in data list:
	print(row dict)
	
#3.关闭连接
cursor.close()
conn.close()
```

```python
import pymysql
# 1.连接MySQL
conn =pymysql.connect(host="127.0.0.1",port=3306, user='root'passwd="rootl23"charset='utf8'，db='unicom')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

# 2.发送指令(***千万不要用字符串格式化去做SQL的拼接，安全隐患SQL注入***)
#cursor.execute("select *from admin where id > 2)
cursor.execute("select *from admin where id > %s",[2,])
# 获取符合条件的第一条数据，得到的是[字典]，没有数据就是none
res = cursor.fetchone()
print(res) #{'id': 3,'password':'qwe123','mobile':'1999999999''username’:'集宁'}
	
#3.关闭连接
cursor.close()
conn.close()
```

#### 4.2.2 删除数据

```python
#1.连接MySQL
conn = pymysql.connect(host="127.0.0.1", port=3386, user='root', passwd="root123", charset='utf8’, db='ynicam')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

# 2.发送指令( *** 千万不要用字符串格式化去做SQL的拼接，安全隐患SQL注入***)
cursor.execute("delete from admin where id=%s",[3,])
conn.commit()

#3.关闭连接
cursor.close()
conn.close()
```

#### 4.2.3 修改数据

```python
#1.连接MySQL
conn = pymysql.connect(host="127.0.0.1", port=3386, user='root', passwd="root123", charset='utf8’, db='ynicam')cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

#2.发送指令( ***千万不要用字符串格式化去做SQL的拼接，安全隐惠SQL注入***）
cursor.execute("update admin set mobile=%s where id=%s",["1888888888",4,])
conn.commit()

#3.关闭连接
cursor.close()
conn.close()
```

强调:

- 在进行 新增、删除、修改时，一定要记得commit，不然数据库么有数据。  
    cursor.execute("…"）  
    conn.commit()
    
- 在查询时，不需要commit，执行fetchone/fetchall  
    cursor.execute("…"）
    
    #第一条数据，字典，无数据时是空列表  
    v1= cursor.fetchone()
    
    #所有数据，列表套字典，无数据时是None  
    v1= cursor.fetchall()
    
- 对于SQL语句不要用Python的字符串格式化进行拼接(会被SQL注入)，一定要用execute+参数
    

```python
cursor.execute(".%s.....%s",["xx","xx" ])
```

