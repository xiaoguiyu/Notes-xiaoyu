

## 一、数据库的基本认识

### 数据库

数据库：
		英文单词DataBase，简称DB。按照一定格式存储数据的一些文件的组合。
		顾名思义：存储数据的仓库，实际上就是一堆文件。这些文件中存储了具有特定格式的数据。

### 数据库管理系统

数据库管理系统：
		DataBaseManagement，简称DBMS。
		**数据库管理系统是专门用来管理数据库中数据的**，数据库管理系统可以
		对数据库当中的数据进行增删改查。

​			常见的数据库管理系统：MySQL、Oracle、MS SqlServer、DB2、sybase等....

### SQL

SQL: 结构化查询语言

通过编写SQL语句，然后DBMS负责执行SQL语句，最终来完成数据库中数据的增删改查操作。

SQL是一套标准，主要学习的就是SQL语句，SQL在mysql中可以使用，
		同时在Oracle中也可以使用，在DB2中也可以使用。

### 数据库数据管理系统和SQL的关系

​		**DBMS--执行--> SQL --操作--> DB**

​	先安装数据库管理系统MySQL，然后学习SQL语句怎么写，编写SQL语句之后，DBMS
​	对SQL语句进行执行，最终来完成数据库的数据管理。

## 二、安装MySQL数据库管理系统

### 步骤

1. 先安装，选择“经典版”
2.  需要进行MySQL数据库实例配置 
3. 注意：一路下一步就行了！！！！！

### 安装需要注意的事项

#### 端口号

1. 端口号port是任何一个软件/应用都会有的，端口号是应用的唯一代表。
2. 端口号通常和IP地址在一块，IP地址用来定位计算机的，端口号port是用来定位计算机上某个服务的/某个应用的！在同一台计算机上，端口号不能重复。具有唯一性。
3. mysql数据库启动的时候，这个服务占有的默认端口号是3306

#### 字符编码

设置mysql数据库的字符编码方式为 UTF8
一定要注意：	**先选中第3个单选按钮，然后再选择utf8字符集。**

#### 配置环境变量

如果没有选择,手动配置

**path=其它路径;C:\Program Files (x86)\MySQL\MySQL Server 5.5\bin**

#### 关于账号密码

mysql超级管理员用户名不能改，一定是：root
		你需要设置mysql数据库超级管理员的密码。
	

设置密码的同时，可以激活root账户远程访问。
		激活：表示root账号可以在外地登录。
		不激活：表示root账号只能在本机上使用。

### 卸载MySQL

1.  双击安装包进行卸载删除。
2. 删除目录：
   		把C:\ProgramData下面的MySQL目录干掉。
      		把C:\Program Files (x86)下面的MySQL目录干掉。

### MySQL服务

位置: 计算机-->右键-->管理-->服务和应用程序-->服务-->mysql服务

关闭和启用MySQL服务的语法:

`net stop 服务名称;`
		 `net start 服务名称;`

###  本地登录的两种方式

1. 显示密码: mysql -uroot -proot
2. 不显示密码: 
   1. mysql -uroot -p 
   2. 输入密码: root



## ✅三、SQL基本知识

### ⭐sql语句的分类

- DQL:  **数据查询语言**（凡是带有select关键字的都是查询语句)

- DML：**数据操作语言**（凡是对**表当中的数据进行增删改**的都是DML）

  insert delete update			

- DDL: **数据定义语言**

  **带有create、drop、alter的都是DDL**

  **DDL主要操作的是表的结构**。不是表中的数据。
  				create：新建，等同于增
  				drop：删除
  				alter：修改
  				这个增删改和DML不同，这个主要是对表结构进行操作

- TCL：

  1. 事务提交：commit;
  2. 事务回滚：rollback;

- DCL:  数据控制语言

  如授权grant、撤销权限revoke....

### SQL常用命令

1. 退出: `exit`
2. 查看数据库: ` show databases; ` **以分号结尾**
3. 创建数据库: `create database 数据库名;`
4. 查看数据库的表: `show tables;`
5. 查看数据库的版本:`select version();`
6. 查看当前使用的数据库: `select database();`

### 表的介绍

#### 什么是表(table)

姓名	性别	年龄**(列：字段)** 

张三	男			20            ------->**行（记录**）
​		 李四	女			21            ------->行（记录）
​		 王五	男			22            ------->行（记录）

数据库当中是以表格的形式表示数据的。
	因为表比较直观。

每一个字段都有：**字段名、数据类型、约束**等属性。
		字段名可以理解，是一个普通的名字，见名知意就行。
		数据类型：字符串，数字，日期等

约束：约束也有很多，其中一个叫做唯一性约束，
			这种约束添加之后，该字段中的数据不能重复

### 关于sql 文件

#### 介绍

xxx.sql这种文件被称为sql脚本文件

sql脚本文件中编写了大量的sql语句。执行sql脚本文件的时候，该文件中所有的sql语句会全部执行！

#### 如何执行sql脚本

`source D:\course\03-MySQL\document\vip.sql`

## ✅四、查询(DQL)

### 简单查询

1. 查看表中的数据: `select * from 表名; `

2. 只查看表结构 `desc 表名;`   不使用缩写: `describe 表名`

3. 查询一个字段: 

   `slect 字段名 from 表名;`

4. 查询多个字段, 使用逗号隔开字段名即可

   `select 字段名1, 字段名2 from 表名;`

5. 查询所有字段: `select * from 表名;`

   缺点: 效率低, 可读性差

6. 给查询的列起名: 

   `select 字段名1, 字段名2 as 自定义名 from 表名`

   例子: `select deptno, dname as deptname from dept;`  其中 as关键字可以省略

   当需要 自定义名中 有空格时, 可以给自定义名 加单引号和双引号

   注意：**在所有的数据库当中，字符串统一使用单引号括起来，
   			单引号是标准，双引号在oracle数据库中用不了。但是在mysql
   			中可以使用**

7. 字段可以使用数学表达式

   例: `select ename, sal * 12  as name_sal from emp; `  工资*12

### 条件查询

语法: `select 字段1, 字段2, 字段3...  from 表名 where 条件;`

#### 条件

示例为名为stu的数据库

1. =等于:

   例: 查询薪资等于800的员工姓名和编号？

    `select empno,ename from emp where sal = 800;`

2. <>或!= 不等于

   例: 查询薪资不等于800的员工姓名和编号？

   `select empno,ename from emp where sal != 800;
   select empno,ename from emp where sal <> 800; `// 小于号和大于号组成的不等号

3. 小于 < 

   例: 查询薪资小于2000的员工姓名和编号？

   ` select empno,ename,sal from emp where sal < 2000;`

4. <= 小于等于

   例: 查询薪资小于等于3000的员工姓名和编号

   `select empno,ename,sal from emp where sal <= 3000;`

5. 大于 > 

   查询薪资大于3000的员工姓名和编号？
   `select empno,ename,sal from emp where sal > 3000;`

6. 大于等于>= 

   查询薪资大于等于3000的员工姓名和编号？
   `select empno,ename,sal from emp where sal >= 3000;`

   **between … and …. 两个值之间, 等同于 >= and <=**

7. is null 为 null（is not null 不为空）

   查询哪些员工的津贴/补助为null？
   ` select empno,ename,sal,comm from emp where comm = null;`

8. and 并且

   查询工作岗位是MANAGER并且工资大于2500的员工信息？

   `select job, ename,sal from emp where sal >2500 && job = 'manager';`

9. or 或者

   查询工作岗位是MANAGER和SALESMAN的员工？

   and和or同时出现  and的优先级高, 会先运算

   **and 和 or 可以使用&& 和 || 代替**  ,注意使用()提升优先级

10. in 包含，相当于多个 or （not in 不在这个范围中）

    查询工作岗位是MANAGER和SALESMAN的员工？

    `select empno,ename,job from emp where job = 'MANAGER' or job = 'SALESMAN';
    select empno,ename,job from emp where job in('MANAGER', 'SALESMAN');`

    **注意: in不是一个区间, in后面的是具体的值**

11. not 可以取非，主要用在 is 或 in 中

12. like: 称为模糊查询，支持%或下划线匹配

    **%匹配任意多个字符下划线：任意一个字符。**（%是一个特殊的符号，_ 也是一个特殊符号）

    找出名字中含有O的？
    `select ename from emp where ename like '%O%';`

    找出名字以T结尾的？
    `select ename from emp where ename like '%T';`

    找出名字以K开始的？
    `select ename from emp where ename like 'K%';`

    找出第二个字每是A的？
    `select ename from emp where ename like '_A%';`

    找出第三个字母是R的？
    `select ename from emp where ename like '__R%';`

### 排序查询

#### order by 

 默认升序排列

1. 查询所有员工薪资，排序？

   `select ename , sal from emp order by sal;`

2.  如何降序	

   `select ename , sal from emp order by sal desc;` 

3. 指定升序:

   `select ename , sal from emp order by sal asc;`

4. 多个字段的排序

   查询员工名字和薪资，要求按照薪资升序，如果薪资一样的话，
   再按照名字升序排列。

   `select ename , sal from emp order by sal asc , ename asc;` 

   sal 在前, 起主导, 只有sal 相等的时候, 才会考虑启用ename 排序

5. 根据字段的位置可以排序

   `select ename,sal from emp order by 2;`   2表示第二列

   这种写法不建议, 不健壮, 列的顺序可能发生改变

   案例: 找出工资在1250到3000之间的员工信息，要求按照薪资降序排列。

   `select ename, sal ,job from emp where sal <= 3000 && sal >= 1250 order by sal;`

## 五、数据处理函数(单行处理函数)

数据处理函数又被称为单行处理函数

### 特点

1. **一个输入对应一个输出**
2. 和单行处理函数相对的是:  多行处理函数(多个输入对应一个输出)

### 常见的单行处理函数

1. lower 转换小写

   将名字转化为小写

   `mysql> select lower(ename) as ename from emp;`

2. upper 转换大写

3. substr 取子串   （substr( 被截取的字符串, 起始下标,截取的长度)）

   找出员工名字第一个字母是A的员工信息？

   `select ename from emp where substr(ename,1,1) = 'A';`

4. concat函数进行字符串的拼接 

   拼接emp表中 名字和 编号

   `select concat(empno,ename) from emp;`

5. lenght 去长度

   名字的长度

   `select length(ename) enamelength from emp;`

6. trim 去空格

   `select * from emp where ename = trim('  KING');`

7. round 四舍五入

   当select后面直接跟 **字面量 和字面值**  会有一个奇怪的现象: 会根据表的结构生成一个全是字面量的表

   例: `select 'abc' from emp;`

   

   `select round(1236.567, 0) as result from emp;`   //保留整数位。

   `select round(1236.567, 1) as result from emp;` //保留1个小数
   `select round(1236.567, 2) as result from emp; `//保留2个小数
   `select round(1236.567, -1) as result from emp; `// 保留到十位, 反向保留

8. rand() 生成随机数

   `select round(rand()*100,0) from emp; `// 100以内的随机数

9. ifnull 可以将 null 转换成一个具体值

   ifnull是空处理函数。专门处理null的。

   注意: 在所有数据库当中，只要有NULL参与的数学运算，最终结果就是NULL

   案例:

   计算每个员工的年薪 : 年薪 = (月薪 + 月补助) * 12

   `select ename, (sal + ifnull(comm, 0)) * 12 as yearsal from emp;`

10. case..when..then..when..then..else..end

    案例: 

    当员工的工作岗位是MANAGER的时候，工资上调10%，当工作岗位是SALESMAN的时候，工资上调50%,其它正常。（注意：不修改数据库，只是将查询结果显示为工资上调）

    `select ename, job, sal as oldsal,
         (case job when 'manager' then sal*1.1 when 'salesman' then sal * 1.5 else sal end) as newSal from emp;`

11. str_to_date 将字符串转换成日期

12. date_format 格式化日期   如下

13. format 设置千分位, 格式化数字

     语法:  format(数字, '格式')
    			`select ename,format(sal, '$999,999') as sal from emp;`

#### date日期函数

1. str_to_date：将字符串varchar类型转换成date类型

2. date_format：将date类型转换成具有一定格式的varchar字符串类型

   

   如果你提供的日期字符串格式为 %Y-%m-%d，str_to_date函数就不需要了！！！
   如果输入的是mysql默认的日期格式：'%Y-%m-%d',  也不需要使用date_format函数

   这两者都会自动进行类型转换

##### MySQL的日期格式

**%Y 年     %m 月   %d 日     %h 时     %i 分      %s 秒**

##### 数据库中的命名规范

所有的标识符都是全部小写，单词和单词之间使用下划线进行衔接

##### date和datetime的区别

1. date是短日期：只包括年月日信息。

2. datetime是长日期：包括年月日时分秒信息

   

   mysql短日期默认格式：%Y-%m-%d
   mysql长日期默认格式：%Y-%m-%d %h:%i:%s

在mysql当中获取系统当前时间使用  `now() `函数

##### 如何计算两个日期的“年差”

> 使用TimeStampDiff()函数																																				  TimeStampDiff(间隔类型, 前一个日期, 后一个日期)
> `timestampdiff(YEAR, hiredate, now())`

### distinct关键字

作用:   把查询结果去除重复记录

##### 注意 : 

1. 原表数据不会被修改，只是查询结果去重。去重需要使用一个关键字：distinct

2. distinct只能出现在所有字段的最前方

3. distinct出现在job,deptno两个字段之前，表示两个字段联合起来去重

   ` select distinct job,deptno from emp;`



## 六、分组函数(多行处理函数/聚合函数)

多行处理函数的特点：输入多行，最终输出一行。

### 分组函数

1. count 记数
2. sum 求和
3. avg	平均值
4. max	最大值
5. min	最小值

#### 注意

分组函数在使用的时候必须先进行分组，然后才能用。
	**如果没有对数据进行分组，整张表默认为一组。**

#### 案例

找出最高工资？
		` select max(sal) from emp;`

计算工资和：
			` select sum(sal) from emp;`

计算平均工资：
		` select avg(sal) from emp;`

计算员工数量？
		` select count(ename) from emp;`

### 分组函数的注意事项

1. 第一点：**分组函数自动忽略NULL，不需要提前对NULL进行处理**

   ` select sum(comm) from emp;`

2. 分组函数中**count(*)** 和 **count(具体字段)**有什么区别？

   **ount(具体字段)：表示统计该字段下所有不为NULL的元素的总数
   **count(*)：统计表当中的总行数**。（只要有一行数据count则++）
   因为每一行记录不可能都为NULL，一行数据中有一列不为NULL，则这行数据就是有效的。

3. **分组函数不能够直接使用在where子句中**

   `select ename,sal from emp where sal > min(sal);`  //**这种写法是错误的**

4. 所有的分组函数可以组合起来一起用

### 分组查询

#### 什么是分组查询

在实际的应用中，可能有这样的需求，需要先进行分组，然后对每一组的数据进行操作。
		这个时候我们需要使用分组查询，怎么进行分组查询呢？

#### 语法

```SQL
select 
		...
	from
		...
	group by
		...
```

#### SQL语句的执行顺序(记住!)

`select ... from .. where ... group by .. order by ..`

以上关键字的顺序不能颠倒, 执行顺序为: 

1. from 

2. where 

3. group by 

4. select 

5. order by 

   

**为什么分组函数不能直接使用在where后面？**

`select ename,sal from emp where sal > min(sal);`//报错。
			因为**分组函数在使用的时候必须先分组之后才能使用。**
			**where执行的时候，还没有分组**。所以where后面不能出现分组函数。
          `select sum(sal) from emp; `
			这个没有分组，为啥sum()函数可以用呢？因为select在group by之后执行

#### 分组函数使用案例

1. 找出每个工作岗位的工资和？

   实现思路: 按照工作岗位分组，然后对工资求和

   ` select sum(sal),job  from  emp group by job;`

2. 找出每个部门的最高薪资

   思路: 先对部门分组, 在求最高薪资

   `select deptno, max(sal)   from emp group by deptno;`

3. 找出“每个部门，不同工作岗位”的最高薪资？

   实现思路: **对部门和工作岗位分组**, 再求最好薪资

   `select deptno, job, max(sal)    from emp group by deptno, job;`

   结论: 在一条select语句当中，如果有group by语句的话，
   			**select后面只能跟：参加分组的字段，以及分组函数**。
   			其它的一律不能跟。

#### having

作用: 使用having可以对分完组之后的数据进一步过滤。

注意: **having不能单独使用，having不能代替where，having必须**
					 **和group by联合使用**

#### having 和 where

**where和having，优先选择where**，where实在完成不了了，再选择having

#### 使用案例

1. 找出每个部门最高薪资，要求显示最高薪资大于3000的？

   思路1: 使用having

   先对部门分组, 在筛选出最高薪资大于3000的

   `select deptno, max(sal) from emp group by deptno having max(sal) > 3000;`

   思路二: 使用where(优先使用) : 先选出薪资大于3000的, 在对部门分组, 然后求出最高薪资

   `select deptno, max(sal)  from emp where sal > 3000  group by deptno;`

2. 找出每个部门平均薪资，要求显示**平均**薪资高于2500的。

   思路: 先对部门分组, 在筛选出平均工资高于2500

   `select  avg(sal), deptno   from emp group by deptno having avg(sal) > 2500;`

   综合案例: 

3. 找出每个岗位的平均薪资，要求显示平均薪资大于1500的，除MANAGER岗位之外，
   	要求按照平均薪资降序排

   思路: 

   1.  先使用where 去除掉manager
   2. 在对岗位进行分组
   3. 然后使用haveing 筛选 平均工资
   4. 再用order by排序

   `select  job, avg(sal) as '平均工资' from emp  where job != 'manager'   group by job having avg(sal) > 1500 order by avg(sal) desc;`

### 总结

⭐单表查询 关键字的顺序

```SQL
select 
	...
		from
    ...
		where
	...
		group by
	...
		having
	...
		order by
	...
```

SQL语句执行的顺序:

1. from
2. where 
3. group by
4. haveing 
5. select 
6. order by

**从某张表中查询数据，先经过where条件筛选出有价值的数据。对这些有价值的数据进行分组。
	分组之后可以使用having继续筛选。select查询出来。最后排序输出!** 

## ⭐七、连接查询  

### 什么是连接查询？

从一张表中单独查询，称为单表查询。
		从emp表和dept表联合起来查询数据，从emp表中取员工名字，从dept表中取部门名字。
		这种跨表查询，多张表联合起来查询数据，被称为连接查询。

### 连接查询的分类

#### 按语法年份分类

1. SQL92:  从92年出现的语法(不推荐使用)

   `select e.ename,d.dname from emp e, dept d where e.deptno = d.deptno;`

   92的缺点: 结构不清晰，表的连接条件，和后期进一步筛选的条件，都放到了where后面。

2. SQL99:  从99年出现的语法

   `select  e.ename,d.dname from emp e join dept d on e.deptno = d.deptno;`

   join前的`inner` 可以省略, 带着可读性更强

   SQL99的优点: 

   表连接的条件是独立的，连接之后，如果还需要进一步筛选，再往后继续添加where

#### 按表的连接方式分类

###### 内连接

1. 等值连接
2. 非等值连接
3. 自连接

###### 外连接：

1. 左外连接（左连接）
2. 右外连接（右连接）

###### 全连接

了解即可

### ⭐笛卡尔积现象

#### 介绍

当两张表进行连接查询，**没有任何条件限制**的时候，最终查询结果条数，是**两张表条数的乘积**，这种现象被称为：笛卡尔积现象。（由笛卡尔发现，这是一个数学现象。）

#### 如何避免笛卡尔积现象

连接时加条件，满足这个条件的记录被筛选出来！

`select ename, dname from emp, dept where emp.deptno = dept.deptno;`

注意: 上面的sql语句并不规范, 需要给表其别名, 效率更高



通过笛卡尔积现象得出，**表的连接次数越多效率越低**，尽量**避免表的连接次数。**

### 内连接

A表和B表连接，AB两张表**没有主次关系**。平等的

内连接的特点：完成能够匹配上这个条件的数据查询出来。

#### ⭐等值连接

案例: 查询每个员工所在部门名称，显示员工名和部门名？

`select e.ename as empname, d.dname as '部门名' from emp e join
     dept d on e.deptno = d.deptno;`

#### 非等值连接

案例: 找出每个员工的薪资等级，要求显示员工名、薪资、薪资等级？

`select e.ename ,e.sal, s.grade from emp e join salgrade s on
e.sal > s.losal and e.sal < s.hisal;`

#### 自连接

技巧: **可以将一张表看成两张表**

###### 案例: 

查询员工的上级领导，要求显示员工名和对应的领导名？

 `select b.ename as '员工名' , a.ename as '领导名' from emp a join emp b on            		              a.empno = b.mgr;`

### 外连接

带有right的是右外连 *+接，又叫做右连接。带有left的是左外连接，又叫做左连接

#### 右连接案例

`select e.ename, d.dname from emp e right  join dept d on e. deptno = d.deptno;`

right代表什么：**表示将join关键字右边的这张表看成主表**，主要是为了将这张表的数据全部查询出来，捎带着关联查询左边的表。在外连接当中，两张表连接，产生了主次关系。

#### 左连接案例

`select e.ename, d.dname from emp e left  join dept d on e. deptno = d.deptno;`

join前的outer可以省略, 带着可读性强

###### 两者的联系: 

任何一个右连接都有左连接的写法。
        任何一个左连接都有右连接的写法

###### 案例

查询每个员工的上级领导，要求显示所有员工的名字和领导名？

`select e.ename as '员工名', a.ename as '领导名' from emp e  left join emp a on e.mgr = a.empno;`

##### 外连接和内连接

外连接的查询结果条数一定是 >= 内连接的查询结果条数

### ⭐多表连查

#### 语法

```sql
select 
			...
		from
			 a
		join
			 b
		on
			a和b的连接条件
		join
			 c
		on
			a和c的连接条件
		right join
			 d
		on
			a和d的连接条件
```

**注意**: **一条SQL中内连接和外连接可以混合。都可以出现！**

#### ✅案例

- 找出每个员工的部门名称以及工资等级，要求显示员工名、部门名、薪资、薪资等级？

思路: 

1. 先求每个员工的部门名称

   `select e.ename, d.dname from emp e join dept d on e.deptno = d.deptno;`

2. 再求每个员工的工资等级

   `select e.ename, s.grade, e.sal from emp e join salgrade s on
    e. sal > losal and e.sal < hisal;`

3. 组合

   ```sql
   select 
   	e.ename , d.deptno , e.sal, s.grade 
       from 
       	emp e 
       join 
       	dept d 
       on
   		e.deptno = d.deptno 
        join 
   		salgrade s on e.sal >= s.losal and e.sal <= s.hisal;
   ```

   

- 找出每个员工的部门名称以及工资等级，还有上级领导，
  要求显示员工名、领导名、部门名、薪资、薪资等级？

  思路: 

  1. 先求每个员工的部门名称

     `select e.ename, d.dname from emp e join dept d on e.deptno = d.deptno;`

  2. 再求每个员工的工资等级

     `select e.ename, s.grade, e.sal from emp e join salgrade s on
      e. sal > losal and e.sal < hisal;`

  3. 然后求出领导名

```sql
select 
a.ename as '员工名', d.dname, a.sal, s.grade, b.ename as '领导名'
   from
   		emp a 
   left join
   		emp b 
   on 
   		a.mgr = b.empno 
   join 
   		dept d 
   on 
   		 a.deptno = d.deptno
   join 
   		salgrade s 
   on 
   		a.sal < s.hisal and a.sal > s.losal;
```

## 八、子查询

### 基本介绍

select语句中嵌套select语句，被嵌套的select语句称为子查询

### 子查询的位置

```sql
select
		..(select).
	from
		..(select).
	where
		..(select).
```

#### where 语句中的子查询

##### 案例

找出比最低工资高的员工姓名和工资？

思路: 

1. 找出最低工资的人员

   `select ename , min(sal) from emp;`

2. 找出 > 800的

   `select ename, sal from emp where sal > 800;`

3. 合并

   `select ename, sal from emp where sal > (select min(sal) from emp);`

#### 🍓from子句中的子查询

**注意：from后面的子查询，可以将子查询的查询结果当做一张临时表**

##### 案例

找出每个岗位的平均工资的薪资等级

思路: 

1. 先没个岗位的平均工资(对job进行分组)

   `select job, avg(sal) from emp group by job;`

2. 将1求出的结果看做为 一张表

3. 使用连接查询 

   ```sql
   select
       s.grade , t.*
       from 
       	(select job, avg(sal) as asal  from emp group by job)  as t
       join
        	salgrade as s
        on
        	t.asal>s.losal and t.asal < s.hisal;
   ```

   

#### 🍅select后面出现的子查询

这个了解即可

##### 案例

找出每个员工的部门名称，要求显示员工名，部门名？

**注意：对于select后面的子查询来说，这个子查询只能一次返回1条结果，**
	    **多于1条，就会报错**

## 九、union 和 limit

### union

#### 基本介绍

union : 会将合并查询结果集

#### 案例

查询工作岗位是MANAGER和SALESMAN的员工？

`select ename,job from emp where job = 'MANAGER' or job = 'SALESMAN';
	select ename,job from emp where job in('MANAGER','SALESMAN');`

使用union 合并: 

`select ename,job from emp where job = 'MANAGER'
	 union
	 select ename,job from emp where job = 'SALESMAN';`

#### union的优点

union的效率要高一些。对于表连接来说，每连接一次新表，则匹配的次数满足笛卡尔积，成倍的翻。但是**union可以减少匹配的次数**。在减少匹配次数的情况下，还可以完成两个结果集的拼接

举例: 

a 连接 b 连接 c
		a 10条记录
		b 10条记录
		c 10条记录
		匹配次数是：1000

a 连接 b一个结果：10 * 10 --> 100次
		  a 连接 c一个结果：10 * 10 --> 100次
		  使用union的话是：100次 + 100次 = 200次。（union把乘法变成了加法运算）

#### union的注意事项

1. union在进行结果集合并的时候，要求两个结果集的列数相同	

   ```sql
   select ename,job from emp where job = 'MANAGER'
   	union
   	select ename from emp where job = 'SALESMAN';  //错误的
   ```

   

2. 注意: oracle在执行时下面的sql语句时, 会报错, 而MySQL则不会,                                                     oracle要求集合并时列和列的数据类型也要一致

   ```sql
   select ename,job from emp where job = 'MANAGER'
   	union  
   	select ename,sal from emp where job = 'SALESMAN';
   ```

   

### ⭐limit 

#### limit的作用

将查询结果集的一部分取出来。通常使用在分页查询当中

分页的作用是为了提高用户的体验，因为一次全部都查出来，用户体验差。
可以一页一页翻页看

#### limit的用法

```SQL
select 
		ename,sal
	from
		emp
	order by 
		sal desc
	limit 5;       //取前5

```

完整用法: 

`limit startIndex, length`
		    startIndex是起始下标，length是长度。起始下标从0开始

注意: 

**mysql当中limit在order by之后执行！！！！！！**

##### 案例: 

1. 取出工资排名在[3-5]名的员工？ 
2. 取出工资排名在[5-9]名的员工？

#### 分页

每页显示3条记录
	第1页：limit 0,3		[0 1 2]
	第2页：limit 3,3		[3 4 5]
	第3页：limit 6,3		[6 7 8]
	第4页：limit 9,3		[9 10 11]

每页显示pageSize条记录
	**第pageNo页：limit (pageNo - 1) * pageSize  , pageSize**

### ⭐查询语句(DQL)的总结

#### 语法

```SQL
select 
		...
	from
		...
	where
		...
	group by
		...
	having
		...
	order by
		...
	limit
		...
```

#### 执行顺序

1. from
2. where
3. group by
4. having
5. select
6. order by
7. limit..

## ✅十 、表

### 表结构的增删改(DDL)

#### 建表

##### 语法

```sql
create table 表名(
		字段名1 数据类型, 
		字段名2 数据类型, 
		字段名3 数据类型
	);
```

表名：建议以t_ 或者 tbl_开始，可读性强。见名知意。字段名：见名知意。
	**表名和字段名都属于标识符**。

##### 案例

创建一个学生表

学号/姓名/年龄/性别/邮箱地址

```sql
create table t_student(
		no int,
		name varchar(32),
		sex char(1),
		age int(3),
		email varchar(255)
	);
```

##### 快速创建表

原理:

将一个查询结果当做一张表新建！！！这个可以完成表的快速复制！！表创建出来，同时表中的数据也存在了！！

使用案例: 

`create table mytable as select empno,ename from emp where job = 'MANAGER';`

#### 表的删除

`drop table t_student;` // 当这张表不存在的时候会报错！

`drop table if exists t_student;`  建议使用这条删除语句,  如果这张表存在的话，删除



#### ❌表的修改

##### 添加字段

`alter table t_student add contact_tel varchar(40);`

##### 修改字段: 

`alter table t_student change student_name student_name varchar(100) ;`

##### 删除字段

`alter table t_student drop contact_tel;`



### MySQL中的数据类型

#### 常见的数据类型

1. varchar (最长255)

   **可变长度的字符串**, 会根据实际的数据长度动态分配空间,节省空间。。															**优点：节省空间缺点：需要动态分配空间，速度慢**

2. char(最长255)

   **定长字符串**
   不管实际的数据长度是多少。分配固定长度的空间去存储数据。																		使用不恰当的时候，可能会导致空间的浪费

   优点：**不需要动态分配空间，速度快**。缺点：使用不当**可能会导致空间的浪费。**

3. int  (最长11)

   数字中的整数型。等同于java的int。

4. bigint

   数字中的长整型。等同于java中的long

5. float

   单精度浮点型数据

6. double

   双精度浮点型数据

7. date   短日期类型

8. datetime  长日期类型

9. clob  字符大对象
   			最多可以存储4G的字符串。
      			比如：存储一篇文章，存储一个说明。
      			超过255个字符的都要采用CLOB字符大对象来存储。Character Large OBject:CLOB

10. blob   二进制大对象
    			Binary Large OBject
    			专门用来存储图片、声音、视频等流媒体数据。
    			往BLOB类型的字段上插入数据的时候，例如插入一个图片、视频等，需要使用IO流才行。

### 对表数据的增删改(DML)

#### 插入数据insert

语法: 

```SQL
insert into 
		表名(字段名1,字段名2,字段名3...) 
	values
		(值1,值2,值3);

```

**注意：字段名和值要一一对应**。什么是一一对应？**数量要对应, 数据类型要对应**

例: 

```sql
insert into 
		t_student(no,name,sex,age,email) 
values(1,'zhangsan','m',20,'zhangsan@123.com');

insert into 
t_student(email,name,sex,age,no) 
values('lisi@123.com','lisi','f',20,2);
```

##### insert语句插入多条记录的方法

语法

```sql
insert into 
	表名(字段名1,字段名2) 
	values (),(),(),();
```

案例

```SQL
nsert into t_user(id,name,birth,create_time) values
		(1,'zs','1980-10-11',now()), 
		(2,'lisi','1981-10-11',now()),
		(3,'wangwu','1982-10-11',now());
```

注意：

1. **insert语句但凡是执行成功了，那么必然会多一条记录。**

   没有给其它字段指定值的话，默认值是NULL

2. insert语句中的 “字段名” 是可以省略, 前面的字段名省略的话，等于都写上了！所以值也要都写上

##### 如何将查询结果插入到一张表中

案例: 

`insert into dept_bak select * from dept; `//很少用！

**插入的数据的类型和表的类型必须一致, 否则会报错**

#### 修改表数据update

##### 语法

```sql
update 表名 set 字段名1=值1,字段名2=值2,字段名3=值3... where 条件;
```

**注意：如果没有条件限制会导致所有数据全部更新**。

例: `update t_use r set name = 'jack', birth = '2000-10-11' where id = 2;`

#### 删除表的数据

##### 语法

```sql
delete from 表名 where 条件;
```

**注意：没有条件，整张表的数据会全部删除！**

例: 

1. `delete from t_user where id = 2;`
2. `delete from t_user; `// 删除所有！

使用delete语句删除数据的方式比较慢, 且delete属于DML语句

delete语句删除数据的原理: 
				表中的数据被删除了，但是这个数据在硬盘上的真实*存储空间不会被释放*！！！
				这种删除**缺点是：删除效率比较低**。  这种删除**优点是：支持回滚(可以再恢复数据！)**

##### truncate

truncate语句也可以删除数据, 但**truncate属于DDL语句**

truncate语句删除数据的原理: 
				这种删除效率比较高，表被一次截断，物理删除。
				这种**删除缺点：不支持回滚。**	这种**删除优点：快速**。'

用法: `truncate table dept_bak; `

## 十一、约束

### 基本介绍

#### 什么是约束

约束：constraint
	在创建表的时候，我们可以给表中的字段加上一些约束，来保证这个表中数据的完整性、有效性！！！	       	**约束的作用就是为了保证：表中的数据有效**！！

#### 约束的分类

1. 非空约束：not null
2. 唯一性约束: unique
3. 主键约束: primary key （简称PK）
4. 外键约束：foreign key（简称FK）
5. 检查约束：check（mysql不支持，oracle支持）

### 非空约束：not null

非空约束not null约束的字段不能为NULL

#### 案例

```SQL
drop table if exists t_vip;
	create table t_vip(
		id int,
		name varchar(255) not null    //not null只有列级约束，没有表级约束！
	);
```

错误的语句: `insert into t_vip(id) values(3);` 有not null约束的字段不能为null

### 唯一性约束: unique

唯一性约束unique约束的字段不能重复，但是**可以为NULL**

#### 案例

```SQL
drop table if exists t_vip;
	create table t_vip(
		id int,
		name varchar(255) unique,
		email varchar(255)
	);
	insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
	insert into t_vip(id,name,email) values(2,'lisi','lisi@123.com');
```

#### 两个字段联合的唯一性

```sql
drop table if exists t_vip;
			create table t_vip(
				id int,
				name varchar(255),
				email varchar(255),
				unique(name,email)    //约束没有添加在列的后面，这种约束被称为表级约束。
			);
			
```

##### 列级约束和表级约束

表级约束: 约束没有添加在列的后面，这种约束被称为表级约束

列级约束: 约束添加载在列后面

表级约束的使用时机: 
			需要给多个字段联合起来添加某一个约束的时候，需要使用表级约束

### ⭐️主键约束: primary key   ★★★★★

#### 基本介绍

​	主键约束：就是一种约束。
​			 主键字段：该字段上添加了主键约束，这样的字段叫做：主键字段
​			 主键值：主键字段中的每一个值都叫做：主键值

##### 什么是主键

​				**主键值是每一行记录的唯一标识。 作用: 主键值是每一行记录的身份证号！！**

**注意: 任何一张表都应该有主键，没有主键，表无效！！**

**主键的特征：not null + unique（主键值不能是NULL，同时也不能重复！）**, **且一张表中只能有一个!!!!!**



主键建议使用的类型: int bigint char

不建议使用：varchar来做主键。主键值一般都是数字，一般都是定长的！

#### 主键的分类:

1. 按键的字段个数分类

   1. 单一主键: 1个字段做主键
   2. 复合主键: 两个字段联合起来做主键

2. 按使用类型分类

   1. 自然主键：主键值是一个自然数，和业务没关系。
   2. 业务主键：主键值和业务紧密关联，例如拿银行卡账号做主键值。这就是业务主键！

   在实际开发中使用的建议
   			自然主键使用比较多，因为主键只要做到不重复就行，不需要有意义。
   			业务主键不好，因为主键一旦和业务挂钩，那么当业务发生变动的时候，
   			可能会影响到主键值，所以业务主键不建议使用。**尽量使用自然主键。**

#### 如何添加主键

##### 案例

```sql
drop table if exists t_vip;
		create table t_vip(
			id int primary key,  //列级约束
			name varchar(255)
		);
		insert into t_vip(id,name) values(1,'zhangsan');
		insert into t_vip(id,name) values(2,'lisi');

```

使用表级约束添加主键: 

```sql
drop table if exists t_vip;
		create table t_vip(
			id int,
			name varchar(255),
			primary key(id)  // 表级约束
		);
```

多个字段联合起来添加主键:

```sql
create table t_vip(
			id int,
			name varchar(255),
			email varchar(255),
			primary key(id,name)
		);
		insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
		insert into t_vip(id,name,email) values(1,'lisi','lisi@123.com');
```



##### 如何自动维护一个主键值

使用auto_increment

案例

```sql
reate table t_vip(
    id int primary key auto_increment, //auto_increment表示自增，从1开始，以1递增！
			name varchar(255)
		);
        insert into t_vip(name) values('zhangsan');
		insert into t_vip(name) values('zhangsan');
		insert into t_vip(name) values('zhangsan');
```

### ⭐外键约束 foreign key  

#### 基本介绍

  外键约束：一种约束（foreign key）
			外键字段：该字段上添加了外键约束
			外键值：外键字段当中的每一个值。

#### ⭐如何添加外键

被外键引用的表称为父表, 使用外键的表称为子表

在设计表时: 

**创建表的顺序是:  先创建父，再创建子。插入数据的顺序是 : 先插入父，再插入子。**

**而删除数据的顺序是:  先删子，再删父。   删除表的顺序是:  先删子，再删父**



理解: 案例

##### 案例

```sql
drop table if exists t_student;
drop table if exists t_class;

create table t_class(
	classno int primary key,
	classname varchar(255)
);
create table t_student(
	no int primary key auto_increment,
	name varchar(255),
	cno int,
	foreign key(cno) references t_class(classno)
);

insert into t_class(classno, classname) values(100, '北京市大兴区亦庄镇第二中学高三1班');
insert into t_class(classno, classname) values(101, '北京市大兴区亦庄镇第二中学高三1班');

insert into t_student(name,cno) values('jack', 100);
insert into t_student(name,cno) values('lucy', 100);
insert into t_student(name,cno) values('lilei', 100);
insert into t_student(name,cno) values('hanmeimei', 100);
insert into t_student(name,cno) values('zhangsan', 101);
insert into t_student(name,cno) values('lisi', 101);
insert into t_student(name,cno) values('wangwu', 101);
insert into t_student(name,cno) values('zhaoliu', 101);

select * from t_student;
select * from t_class;
```

## ❌十一、存储引擎

### 基本介绍

#### 什么是存储引擎

存储引擎是MySQL中特有的一个术语，其它数据库中没有. **存储引擎是一个表存储/组织数据的方式。**
	不同的存储引擎，表存储数据的方式不同

#### 如何给表添加/指定存储引擎

 在建表的时候可以在最后小括号的")"的右边使用：
		  ENGINE来指定存储引擎。CHARSET来指定这张表的字符编码方式。

使用`show create table 表名` 来查看此表的存储引擎和字符编码格式

```sql
create table t_product(
		id int primary key,
		name varchar(255)
	)engine=InnoDB default charset=gbk;
```

### mysql中常见的存储引擎

使用命令:  show engines \g 来查看mysql中支持的存储引擎

1. InnoDB存储引擎
2. MyISAM存储引擎
3. MEMORY存储引擎

#### InnoDB存储引擎

InnoDB存储引擎是*mysql默认的存储引擎*，同时也是一个重量级的存储引擎

##### 主要特征

1. 每个 InnoDB 表在数据库目录中以.frm 格式文件表示
2.  InnoDB 表空间 tablespace 被用于存储表的内容（表空间是一个逻辑名称。表空间存储数据+索引。）
3. 提供一组用来记录事务性活动的日志文件用 COMMIT(提交)、SAVEPOINT 及ROLLBACK(回滚)支持事务处理
4. 在 MySQL 服务器崩溃后提供自动恢复
   

#####   特点

- InnoDB最大的特点就是支持事务：
  以保证数据的安全,效率不是很高，并且也不能压缩,不能转换为只读，不能很好的节省存储空间。

#### MyISAM存储引擎

InnoDB存储引擎管理的表具有以下特征: 

- 使用三个文件表示每个表：
  1. 格式文件 — 存储表结构的定义（mytable.frm）
  2. 数据文件 — 存储表行的内容（mytable.MYD）
  3. 索引文件 — 存储表上索引（mytable.MYI）：索引是一本书的目录，缩小扫描范围，提高查询效率的一种机制。可被转换为压缩、只读表来节省空间

提示: 对于一张表来说，只要是有主键，或者加有unique约束的字段上会自动创建索引

- MyISAM存储引擎特点：
  	**可被转换为压缩、只读表来节省空间.** 这是这种存储引擎的优势！！！！

#### MEMORY存储引擎

使用 MEMORY 存储引擎的表，其数据存储在内存中，且行的长度固定，
	这两个特点使得 MEMORY 存储引擎非常快

##### 主要特征

1. 在数据库目录内，每个表均以.frm 格式的文件表示。
2. 表数据及索引被存储在内存中。（目的就是快，查询快！）
3. 表级锁机制。
4. 不能包含 TEXT 或 BLOB 字段

##### 特点

MEMORY引擎优点：查询效率是最高的。不需要和硬盘交互

MEMORY引擎缺点：不安全，关机之后数据消失。因为数据和索引都是在内存当中

## ⭐️十二、事务  ★★★★★

### 基本介绍

#### 什么是事务

一个事务其实就是一个完整的业务逻辑。是一个最小的工作单元。不可再分

##### 完整的业务逻辑

假设转账，从A账户向B账户中转账10000.将A账户的钱减去10000（update语句）将B账户的钱加上10000（update语句）这就是一个完整的业务逻辑

以上的操作是一个最小的工作单元，要么同时成功，要么同时失败，不可再分。
		这两个update语句要求**必须同时成功或者同时失败**，这样才能保证钱是正确的

##### 事务的关联

DML语句才会有事务这一说，其它语句和事务无关！！！**insert delete update**
	只有以上的三个语句和事务有关系，其它都没有关系

### 事务的执行过程

InnoDB存储引擎：提供一组用来记录事务性活动的日志文件

在事务的执行过程中，每一条DML的操作都会记录到“事务性活动的日志文件”中。
	在事务的执行过程中，我们可以提交事务，也可以回滚事务。

#### 提交事务

​     **清空事务性活动的日志文件，将数据全部彻底持久化到数据库表中**。
​		提交事务**标志着，事务的结束。并且是一种全部成功的结束**

#### 回滚事务

​		**将之前所有的DML操作全部撤销**，并且**清空事务性活动的日志文件**
​		**回滚事务标志着，事务的结束。并且是一种全部失败的结束**。

#### 如何提交事务和回滚事务

##### 注意: 

**mysql默认是自动提交事务的。（自动提交）**

什么是自动提交:    每执行一条DML语句，则提交一次！

关闭mysql的自动提交机制:    `start transaction;`

自动提交实际上是不符合我们的开发习惯，因为一个业务通常是需要多条DML语句共同执行才能完成的，为了保证数据的安全，必须要求同时成功之后再提交，所以不能执行一条就提交一条

回滚事务的操作演示:

1. 关闭关闭mysql的自动提交机制:    `start transaction;`

2. 向表中插入两条数据

   ```sql
   insert into t_stu values('jack',22, 'm', 2111);
   insert into t_stu values('smith',18, 'm', 2111);
   ```

3. 执行回滚操作: `rollback;`

再次查询此表会发现:  表中的数据已经会到上一次提交点

提交事务演示: 

1. 关闭关闭mysql的自动提交机制:    `start transaction;`

2. 向表中插入两条数据

   ```sql
   insert into t_stu values('jack',22, 'm', 2111);
   insert into t_stu values('smith',18, 'm', 2111);
   ```

3. 执行提交操作: `commit;`

再次查询此表会发现:  表中的数据已经添加

### 事务的特性

1. A：原子性
   		说明事务是最小的工作单元。不可再分。
2. C：一致性
   	所有事务要求，在同一个事务当中，所有操作必须同时成功，或者同时失败，以保证数据的一致性。
3. I：**隔离性**
   	A事务和B事务之间具有一定的隔离。
      	教室A和教室B之间有一道墙，这道墙就是隔离性。
      	A事务在操作一张表的时候，另一个事务B也操作这张表会那样
4. D：持久性
   	事务最终结束的一个保障。事务提交，就相当于将没有保存到硬盘上的数据保存到硬盘上！

#### ⭐事务的隔离性  

##### 事务和事务之间的隔离级别

1. 读未提交：read uncommitted（最低的隔离级别）《没有提交就读到了》

   1. 读未提交:  事务A可以读取到事务B未提交的数据。
   2. 存在的问题就是：
      脏读现象！(Dirty Read):   读到了脏数据。
      这种隔离级别一般都是理论上的，大多数的数据库隔离级别都是二档起步！

2. 读已提交：read committed《提交之后才能读到》

   1. 读已提交: 事务A只能读取到事务B提交之后的数据。
   2. 读已提交解决的问题: 解决了脏读的现象
   3. 存在的问题: 不可重复读取数据。
   4. 不可重复读取数据: 
            在事务开启之后，第一次读到的数据是3条，当前事务还没有结束，可能第二次再读取的时候，读到的数据是4条，3不等于4 ,称为不可重复读取。这种隔离级别是比较真实的数据，每一次读到的数据是绝对的真实。
         	oracle数据库默认的隔离级别是：read committed

3. 可重复读：repeatable read   《提交之后也读不到，永远读取的都是刚开启事务时的数据》

   1. 可重复读取: 

      事务A开启之后，不管是多久，每一次在事务A中读取到的数据都是一致的。即使事务B将数据已经修改，并且提交了，事务A读取到的数据还是没有发生改变，这就是可重复读

   2. 可重复读解决的问题: 解决了不可重复读取数据。

   3. 可重复读存在的问题:  可以会出现幻影读。
      		每一次读取到的数据都是幻象。不够真实！   早晨9点开始开启了事务，**只要事务不结束**，到晚上9点，读到的数据还是那样！读到的是假象。不够绝对的真实。

4. 序列化/串行化：serializable（最高的隔离级别）  
   	这是最高隔离级别，效率最低。解决了所有的问题。
      	这种隔离级别表示事务排队，不能并发！
      	synchronized，线程同步（事务同步）
      	每一次读取到的数据都是最真实的，并且效率是最低的

**mysql中默认的事务隔离级别为可重复读：repeatable read**

## 十二、索引和视图

### 索引(index)

#### 基本介绍

###### 索引

​	**索引是在数据库表的字段上添加的**，是为了提高查询效率存在的一种机制。一张表的一个字段可以添加一个索引，当然，多个字段联合起来也可以添加索引。索引相当于一本书的目录，是为了缩小扫描范围而存在的一种机制。

对于一本字典来说，查找某个汉字有两种方式：

1. 一页一页挨着找，直到找到为止，这种查找方式属于**全字典扫描**。**效率比较低。**
2. 第二种方式：先通过目录（索引）去定位一个大概的位置，然后直接定位到这个位置，做局域性扫描，缩小扫描的范围，快速的查找。这种查找方式属于通过**索引检索**，**效率较高**

MySQL查询方面主要的两种方式: 

1. 全表扫描
2. 索引检索。

###### 注意: 

**在mysql数据库当中索引也是需要排序的**，并且这个索引的排序和TreeSet数据结构相同。TreeSet（TreeMap）底层是一个自平衡的二叉树！**mysql当中索引是一个B-Tree数据结构** , 遵循左小右大原则存放。采用中序遍历方式遍历取数据

#### 索引的实现原理

1. 在任何数据库当中**主键上都会*自动*添加索引对象**，id字段上自动有索引，因为id是PK。另外在mysql当中，一个字段上如果有unique约束的话，也会自动创建索引对象。

2. 在任何数据库当中，任何一张表的任何一条记录在硬盘存储上都

   有一个硬盘的物理存储编号

3. 在mysql当中，索引是一个单独的对象，不同的存储引擎以不同的形式存在

   1. 在MyISAM存储引擎中，索引存储在一个.MYI文件中。
   2. 在InnoDB存储引擎中索引存储在一个逻辑名称叫做tablespace的当中。
   3. 在MEMORY存储引擎当中索引被存储在内存当中。
   4. **不管索引存储在哪里，索引在mysql当中都是一个树的形式存在。（自平衡二叉树：B-Tree）**

   ![](MySQL.assets/索引的实现原理.png)

#### 添加索引的条件

1. 数据量庞大（到底有多么庞大算庞大，这个需要测试，因为每一个硬件环境不同）
2. 该字段经常出现在where的后面，以条件的形式存在，也就是说这个字段总是被扫描。
3. 该字段很少的进行DML(insert delete update)操作。（因为DML之后，索引需要重新排序。）

注意: 

不要随意添加索引，因为索引也是需要维护的，太多的话反而会降低系统的性能。建议通过主键查询，和通过unique约束的字段进行查询，效率是比较高的

#### 索引的创建和删除

##### 创建索引: 

`create index emp_ename_index on emp(ename);`																										 	给emp表的ename字段添加索引，起名：emp_ename_index

##### 删除索引

`drop index emp_ename_index on emp;`
		将emp表上的emp_ename_index索引对象删除。

#### 查看SQL语句的索引检索

在mysql当中，怎么查看一个SQL语句是否使用了索引进行检索？

使用指令: `explain select * from emp where ename = 'KING';`

输出的内容中  type表示的是使用何种类型的检索: 

1. all: 全表扫描
2. ref: 使用索引检索

#### 🍓索引失效常见的几种情况

失效的几种情况: 

1. 模糊匹配当中以“%”开头了

   `select * from emp where ename like '%T';`

   ename上即使添加了索引，也不会走索引，为什么？
   原因是因为**模糊匹配当中以“%”开头了**！尽量避免模糊查询的时候以“%”开始。这是一种优化的手段/策略

2. 使用or的时候

   `explain select * from emp where ename = 'KING' or job = 'MANAGER';`

   如果使用or那么要求or两边的条件字段都要有索引，才会走索引，如果其中一边有一个字段没有索引，那么另一个字段上的索引也会实现。所以这就是为什么不建议使用or的原因

3. 使用复合索引的时候，没有使用左侧的列查找，索引失效

   `reate index emp_job_sal_index on emp(job,sal); 
   explain select * from emp where job = 'MANAGER';`

   复合索引:  两个字段，或者更多的字段联合起来添加一个索引，叫做复合索引

4. 在where当中索引列参加了运算，索引失效

   `create index emp_sal_index on emp(sal);`

   `explain select * from emp where sal + 1 = 800;`

5. 在where当中索引列使用了函数

   `explain select * from emp where lower(ename) = 'smith';`

#### 索引的分类

索引是各种数据库进行优化的重要手段。优化的时候优先考虑的因素就是索引

索引在数据库中的分类: 

- 1. 单一索引：一个字段上添加索引。
  2. 复合索引：两个字段或者更多的字段上添加索引
  3. 主键索引：主键上添加索引。
  4. 唯一性索引：具有unique约束的字段上添加索引

注意：唯一性比较弱的字段上添加索引用处不大

### 视图 view

#### 基本介绍

view:站在不同的角度去看待同一份数据。

#### 如何创建视图和删除视图

创建视图对象：
		`create view dept2_view as select * from dept2;`

删除视图对象：
		`drop view dept2_view;`

#### 视图的作用

方便，简化开发，利于维护

**我们可以面向视图对象进行增删改查，对视图对象的增删改查，会导致
	原表被操作**！（视图的特点：**通过对视图的操作，会影响到原表数据**。）

假设有一条非常复杂的SQL语句，而这条SQL语句需要在不同的位置上反复使用。
这时可以把这条复杂的SQL语句以视图对象的形式新建。在需要编写这条SQL语句的位置直接使用视图对象，可以大大简化开发。并且利于后期的维护，因为修改的时候也只需要修改一个位置就行，只需要修改视图对象所映射的SQL语句。

##### 案例: 

面向视图查询
	`select * from dept2_view; `

面向视图插入
`insert into dept2_view(deptno,dname,loc) values(60,'SALES', 'BEIJING');`

查询原表数据
`mysql> select * from dept2;`        原表的数据的数据也会发生相应的改变

在面向视图开发的时候，使用视图的时候可以像使用table一样。可以对视图进行增删改查等操作。视图不是在内存当中，视图对象也是存储在硬盘上的，不会消失。

#### 使用视图的注意事项

1. 创建视图对应的语句只能是DQL(查询)语句
2. 视图对象创建完成之后，可以对视图进行增删改查等操作, 影响原表的数据

## ❌十三、DBA

### DBA常用命令

#### 数据的导出

1. 在windows的dos命令窗口中：

2. 输入指令: `mysqldump bjpowernode>D:\bjpowernode.sql -uroot -p123456`
   		

   可以导出指定的表吗
   	`mysqldump bjpowernode emp>D:\bjpowernode.sql -uroot -p123456`

#### 数据的导入

##### 步骤

1. 先登录到mysql数据库服务器上。
2. 创建数据库：`create database bjpowernode;`
3. 使用数据库：`use bjpowernode`
4. 然后初始化数据库：`source D:\bjpowernode.sql`

## ⭐十四、数据库设计三范式

### 基本介绍

#### 什么是数据库设计范式

**数据库表的设计依据**。教你怎么进行数据库表的设计

### ✅数据库设计范式   (熟记)

#### 第一范式

> **要求任何一张表必须有主键，每一个字段原子性不可再分**

##### 案例

以新建学生表为例: 

| 学生编号 | 学生姓名 |         联系方式         |
| :------: | :------: | :----------------------: |
|   1001   |   张三   | zs@gmail.com,1359999999  |
|   1002   |   李四   | ls@gmail.com,13699999999 |
|   1001   |   王五   |  ww@163.net,13488888888  |

以上是学生表，并不满足第一范式
		第一：没有主键。第二：联系方式可以分为邮箱地址和电话

修改: 

将学生编号设为主键, 并将练习方式拆分, 修改后符合第一范式

| 学生编号(pk) | 学生姓名 |   邮箱地址   | 联系电话    |
| :----------: | :------: | :----------: | ----------- |
|     1001     |   张三   | zs@gmail.com | 1359999999  |
|     1002     |   李四   | ls@gmail.com | 13699999999 |
|     1003     |   王五   |  ww@163.net  | 13488888888 |

#### 第二范式

> 建立在第一范式的基础之上，**要求所有非主键字段必须完全依赖主键，不要产生部分依赖**
>

###### 案例: 

以新建学生老师信息表为例:

| 学生编号 | 学生姓名 | 教师编号 | 教师姓名 |
| :------: | :------: | :------: | :------: |
|   1001   |   张三   |   001    |  王老师  |
|   1002   |   李四   |   002    |  赵老师  |
|   1003   |   王五   |   001    |  王老师  |
|   1001   |   张三   |   002    |  赵老师  |

这张表描述了学生和老师的关系：（1个学生可能有多个老师，1个老师有多个学生）
这是非常典型的：多对多关系！

以上的表并不满足第一范式



修改以满足第第一范式 :   将学生编号+教师编号设计为主键

| 学生编号 | 教师编号 | 学生姓名 | 教师姓名 |
| :------: | :------: | :------: | :------: |
|   1001   |   001    |   张三   |  王老师  |
|   1002   |   002    |   李四   |  赵老师  |
|   1003   |   001    |   王五   |  王老师  |
|   1001   |   002    |   张三   |  赵老师  |

学生编号+教师编号，两个字段联合做主键，复合主键（PK: 学生编号+教师编号）经过修改之后，以上的表满足了第一范式。但是满足第二范式吗？不满足，“张三”依赖1001，“王老师”依赖001，显然产生了部分依赖。产生部分依赖有什么缺点？数据冗余了。空间浪费了。“张三”重复了，“王老师”重复了。



为了让以上的表满足第二范式，需要这样设计

使用三张表来表示多对多的关系！！！！

**学生表**

| 学生编号(pk) | 学生名字 |
| :----------: | :------: |
|     1001     |   张三   |
|     1002     |   李四   |
|     1003     |   王五   |

**教师表**

| 教师编号(pk) | 教师名字 |
| :----------: | :------: |
|     001      |  王老师  |
|     002      |  赵老师  |

**学生教师关系表**

| id(pk) | 学生编号 | 教师编号 |
| ------ | -------- | -------- |
| 1      | 1001     | 001      |
| 2      | 1002     | 002      |
| 3      | 1003     | 001      |
| 4      | 1001     | 002      |

多对多表的设计: **多对多，三张表，关系表两个外键！！！❗ **

#### 第三范式

> 第三范式建立在第二范式的基础之上, 
>
> 要求所有非主键字段必须直接依赖主键，不要产生传递依赖

##### 案例

以班级学生表为例: 

| 学生编号(pk) | 学生姓名 | 班级编号 |  班级姓名  |
| :----------: | :------: | :------: | :--------: |
|     1001     |   张三   |    01    | 一年级一班 |
|     1002     |   李四   |    02    | 一年级二班 |
|     1003     |   王五   |    03    | 一年级三班 |
|     1004     |   赵六   |    03    | 一年级三班 |

以上表的设计是描述：班级和学生的关系。很显然是1对多关系！一个教室中有多个学生

上表是满足第一范式的，有主键																																						上表也是满足第二范式的, 因为主键不是复合主键，没有产生部分依赖。主键是单一主键								   	但不符合第三范式的要求。一年一班依赖01，01依赖1001，产生了传递依赖, 产生了数据的冗余

修改

**班级表** : 一

| 班级编号(pk) |  标记名称  |
| :----------: | :--------: |
|      01      | 一年级一班 |
|      02      | 一年级二班 |
|      03      | 一年级三班 |

**学生表**: 多

将班级编号设为外键

| 学生编号(pk) | 学生姓名 | 班级编号(fk) |
| :----------: | :------: | :----------: |
|     1001     |   张三   |      01      |
|     1002     |   李四   |      02      |
|     1003     |   王五   |      03      |
|     1004     |   赵六   |      03      |

一对多表的设计: **一对多，两张表，多的表加外键！！！！**

### ⭐表的设计

#### 总结

1. 一对多：
   		一对多，两张表，多的表加外键！！！！！

2. 多对多：
   	多对多，三张表，关系表两个外键！！！！！！

3. 一对一: 

   一对一，外键唯一！！！！

一对一为什么需要拆分表: 

在实际的开发中，可能存在一张表字段太多，太庞大。这个时候就需要拆分表

注意: 

1. 数据库设计三范式是理论上的。实践和理论有的时候有偏差。
2. 最终的目的都是为了满足客户的需求，有的时候会拿冗余换执行速度。因为在sql当中，表和表之间连接次数越多，效率越低（笛卡尔积）,  有的时候可能会存在冗余，但是为了减少表的连接次数，这样做也是合理的，并且对于开发人员来说，sql语句的编写难度也会降低。

 
