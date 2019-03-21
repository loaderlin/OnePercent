# SQL

B - (A ∩ B)

```sql
SELECT
    b.*
FROM
    B_table b
LEFT JOIN A_table a ON b.Bid = a.Bid
WHERE
     a.Aid IS NULL

SELECT
    b.*
FROM
    B_table b
WHERE
    b.Bid NOT IN (
        SELECT
            b.Bid
        FROM
            B_table b
        INNER JOIN A_table a ON b.Bid = a.Bid
    )
```
平均分大于80分的学生，并按平均分分数从大到小排列

```sql
SELECT
    t.student_name,
    avg(t.score)
FROM
    course t
GROUP BY
    t.student_id
HAVING
    avg(t.score) > 80
ORDER BY
    avg(t.score) DESC
```

Oracle SQL: Update a table with data from another table

```sql
UPDATE table1 t1
SET (NAME, DESC) = (
    SELECT
        t2. NAME,
        t2. DESC
    FROM
        table2 t2
    WHERE
        t1. ID = t2. ID
)
WHERE
    EXISTS (
        SELECT
            1
        FROM
            table2 t2
        WHERE
            t1. ID = t2. ID
    )

update t1 
set t1.colmun = t2.column
from table t1,table t2
where t1.id = t2.id

UPDATE CS_ORDER o
SET (o.CUSTOMER_ID) = (
    SELECT
        c. ID
    FROM
        CS_CUSTOMER c
    WHERE
        o.CUSTOMER_CODE = c.CUSTOMER_CODE
        and c.company_id = o.company_id
)
WHERE o.CUSTOMER_ID IS NULL
```

MySQL 

```sql
UPDATE a_table a,
 b_table b
SET a. CODE = b. CODE
WHERE
    a.id = b.id
```

## Oracle 查询优化

```sql
create table rocky_emp(
    id number(11) primary key,
    emp_no number(11) null,
    emp_name varchar2(64 byte) null, 
    job varchar2(32 byte) null, 
    mgr number(11) null,
    hiredate date  null,
    sal number(18, 8) null,
    comm number(18, 8) null,
    deptno number(11) null, 

    tenancy number(11) null,
    creator varchar2(32 byte)  null ,
    create_time date  null ,
    modifier varchar2(32 byte) null ,
    modify_time date  null ,
    rec_ver number(11) null ,
    company_id varchar2(32 byte) null 
)
logging
nocompress
nocache;
comment on table rocky_emp is '薪资结构表';
comment on column rocky_emp.id is '主键';
comment on column rocky_emp.emp_no is '编号';
comment on column rocky_emp.emp_name is '名称';
comment on column rocky_emp.job is '工作';
comment on column rocky_emp.mgr is '主管';
comment on column rocky_emp.hiredate is '聘用日期';
comment on column rocky_emp.sal is '工资';
comment on column rocky_emp.comm is '提成';
comment on column rocky_emp.deptno is '部门编码';

comment on column rocky_emp.tenancy is 'tenancy';
comment on column rocky_emp.creator is '创建人';
comment on column rocky_emp.create_time is '创建时间';
comment on column rocky_emp.modifier is '修改人';
comment on column rocky_emp.modify_time is '修改时间';
comment on column rocky_emp.rec_ver is '版本';
comment on column rocky_emp.company_id is '公司id';
-- 序列
create sequence seq_rocky_emp
minvalue 1 maxvalue 99999999999999
start with 100 increment by 1 cache 20;    
```

基础篇

```sql
is (not) null  -- 查找空值

rownum -- 限制返回行数

listagg(ename, ',') within group(order by ename)  -- 将字符串连接起来

coalesce(c1, c2, c3, c4, c5) -- 返回多个值中第一个不为空的值 <==> nvl(nvl(nvl(nvl(c1, c2), c3), c4), c5)

select name || ' 的工作是 ' || job as msg  from emp -- 拼接列

SUBSTR(str, pos, len) -- 截取某个字段值的 substr

TRANSLATE(expr, from_string, to_string) -- 替换 translate

translate(r.emp_name, '1AEIOU', '1') <==> regexp_replace(r.emp_name, '[AEIOU]')

Oracle 默认排序空值在后面
order by nulls first 
order by nulls last

字符串文字中包含引号
select * from ROCKY_EMP r where r.EMP_NAME = q'[g'day mate]'

计算字符在字符串中出现个次数

select regexp_count(r.EMP_NAME, '''\$') from ROCKY_EMP r where r.EMP_NAME = q'[g'$day mate aaa]'

regexp_like 正则表达式

regexp_like(str, '16*')


regexp_substr(v.name, '[^.]+', 1, 2)
匹配不包含.的多个字符           长度 位置
192.168.0.104 ===>>> 168
```

在where子句中引用取别名的列

```sql
select *
from (select sal as a_asl,comm as a_comm from emp) x
where a_asl < 1000;
```

select中使用逻辑条件

```sql
select grade, count(*)
from (
select(
    case
        when sal <= 1000 then '0-1000'
        when sal <= 2000 then '1000-2000'
        when sal <= 3000 then '2000-3000'
        when sal <= 5000 then '3000-5000'
        when sal <= 8000 then '5000-8000'
    else '好高啊' end
) as grade, epm_name, sal from ROCKY_EMP) x
group by grade
order by 1
```

随机返回N条语句

先随机再取数据

```sql
SELECT * FROM (select * from ROCKY_EMP ORDER by dbms_random.value()) where ROWNUM <= 3;
```

自关联

```sql
select 员工.empno, 员工.ename, 员工.mgr, 主管.empno, 主管.ename 
from emp 员工
left join emp 主管 on (员工.mgr = 主管.empno)
order by 1;

```

```sql
create table rocky_emp_bonus(
    id number(11) primary key,
    emp_no number(11) null,
    received date  null,
    type number(18, 8) null,

    tenancy number(11) null,
    creator varchar2(32 byte)  null ,
    create_time date  null ,
    modifier varchar2(32 byte) null ,
    modify_time date  null ,
    rec_ver number(11) null ,
    company_id varchar2(32 byte) null 
)
logging
nocompress
nocache;
comment on table rocky_emp_bonus is '奖金表';
comment on column rocky_emp_bonus.id is '主键';
comment on column rocky_emp_bonus.emp_no is '编号';
comment on column rocky_emp_bonus.received is '接受时间';
comment on column rocky_emp_bonus.type is '奖金类型';

comment on column rocky_emp_bonus.tenancy is 'tenancy';
comment on column rocky_emp_bonus.creator is '创建人';
comment on column rocky_emp_bonus.create_time is '创建时间';
comment on column rocky_emp_bonus.modifier is '修改人';
comment on column rocky_emp_bonus.modify_time is '修改时间';
comment on column rocky_emp_bonus.rec_ver is '版本';
comment on column rocky_emp_bonus.company_id is '公司id';
-- 序列
create sequence seq_rocky_emp_bonus
minvalue 1 maxvalue 99999999999999
start with 100 increment by 1 cache 20;    
```

聚集与连接

左连接时 右表有多条数据，左表也要显示多条数据
先聚集 奖金累加 0.3 然后乘以基本工资再求和

```sql
SELECT
    e.DEPTNO,
    sum(e.sal),
    sum(e.sal * eb2.rate) 
FROM
    ROCKY_EMP e
LEFT JOIN (
    SELECT
        eb.EMP_NO,
        sum(
            CASE
                WHEN eb.type = 1 THEN
                0.1 
                WHEN eb.type = 2 THEN
                0.2 
                WHEN eb.type = 3 THEN
                0.3 
            END 
        ) AS rate 
    FROM
        ROCKY_EMP_BONUS eb 
    GROUP BY eb.EMP_NO ) eb2 ON e.EMP_NO = eb2.EMP_NO 
GROUP BY e.DEPTNO
```

提取首字母

```sql
select UPPER(substr(regexp_replace(r.EMP_NAME, '([[:alpha:]])(.*)', '\1'), 1, 1)) || LOWER(SUBSTR(regexp_replace(r.EMP_NAME, '([[:alpha:]])(.*)', '.\2'),1)) as Emp_name from ROCKY_EMP r;

<==>

select regexp_replace(INITCAP(r.EMP_NAME), '([[:alpha:]])(.*)', '\1.\2') as Emp_name from ROCKY_EMP r;

更新

update ROCKY_EMP r
set r.EMP_NAME = 
(select regexp_replace(INITCAP(r.EMP_NAME), '([[:alpha:]])(.*)', '\1.\2') as Emp_name from ROCKY_EMP rs where r.EMP_NO = rs.EMP_NO)
where r.EMP_NAME is not null
```

生成累计

```sql
SELECT
    f.id,
    TOTAL_AMOUNT as 单条合计,
    sum( TOTAL_AMOUNT ) over ( ORDER BY f.id ) AS 成本累计 
FROM
    "CS_DISPATCH_FEE" f 
WHERE
    fee_name = '运费' 
ORDER BY
    f.id
```

## 实战

SQL查询某一字段唯一值及其记录条数的语句

```sql
select t.user_name, count(t.user_name) from SYS_USER t group by t.user_name
```

根据 数据字典 直接更新 证件表的Code
```sql
update CS_CERTIFICATE t
set t.CERTIFICATE_CODE = (
    select s.DS_CODE from SYS_DICT_SPEC s where s.DS_VALUE = t.CERTIFICATE_NAME
)
```

获取 数据字典中的Code 显示

```sql
SELECT
    t.PARTS_CODE as 配件编码,
    t.PARTS_NAME as 配件名称,
    ( SELECT y.DS_VALUE FROM SYS_DICT_SPEC y WHERE y.DS_TYPE = 'parts_type' AND y.DS_CODE = t.PARTS_TYPE ) as 配件类型
FROM
    "CS_PARTS_RECLAIM" t
```

计算备用金

```sql
SELECT
    t.driver_id,
    sum( CASE WHEN t.OPERATE_TYPE = '10' THEN - t.TOTAL_AMOUNT ELSE t.TOTAL_AMOUNT END )
FROM
    CS_SPARE_MONEY_LOG t
GROUP BY
    t.DRIVER_ID
ORDER BY
    t.driver_id
```

Insert Into

```sql
INSERT INTO
A_table (Id, vehicle_no ...)
SELECT
SEQ_A_table.nextval, x.vehicle_no
FROM
(
    select xxx as vehicle_no
    from A_table
) x
```

数据库的三级模式结构，它包括外模式，概念模式，内模式，有效地组织，管理数据，提高了数据库的逻辑独立性和物理独立性。

在SQL语言中，我们可以使用两个通配符%和_，其中"%"表示0个或多个字符，而"_"则表示一个字符。

数据独立性是指应用程序和数据结构之间相互独立，互不影响。在三层模式体系结构中数据独立性是指数据库系统在某一层次模式上的改变上不会使它的上一层模式也发生改变的能力

1. 概念结构设计。这是数据库设计的第一个阶段，在管理信息系统的分析阶段，已经得到了系统的数据流程图和数据字典，现在要结合数据规范化的理论，用一种数据模型将用户的数据需求明确地表示出来。

概念数据模型是面向问题的模型，反映了用户的现实工作环境，是与数据库的具体实现技术无关的。建立系统概念数据模型的过程叫做概念结构设计。

2. 逻辑结构设计。根据已经建立的概念数据模型，以及所采用的某个数据库管理系统软件的数据模型特性，按照一定的转换规则，把概念模型转换为这个数据库管理系统所能够接受的逻辑数据模型。不同的数据库管理系统提供了不同的逻辑数据模型，如层次模型、网状模型、关系模型等。

3. 物理结构设计。为一个确定的逻辑数据模型选择一个最适合应用要求的物理结构的过程，就叫做数据库的物理结构设计。数据库在物理设备上的存储结构和存取方法称为数据库的物理数据模型。

- 避免活锁： 先来先服务
- 防止死锁： 一次封锁，顺序封锁

1. 活锁

如果事务T1封锁了数据R，事务T2又请求封锁R，于是T2等待。T3也请求封锁R，当T1释放了R上的封锁之后系统首先批准了T3的请求，T2仍然等待。然后T4又请求封锁R，当T3释放了R上的封锁之后系统又批准了T4的请求，...，T2有可能永远等待，这就是活锁的情形，如图8.4(a)所示。 避免活锁的简单方法是采用先来先服务的策略。

2. 死锁

如果事务T1封锁了数据R1，T2封锁了数据R2，然后T1又请求封锁R2，因T2已封锁了R2，于是T1等待T2释放R2上的锁。接着T2又申请封锁R1，因T1已封锁了R1，T2也只能等待T1释放R1上的锁。这样就出现了T1在等待T2，而T2又在等待T1的局面，T1和T2两个事务永远不能结束，形成死锁。

### 死锁的预防

在数据库中，产生死锁的原因是两个或多个事务都已封锁了一些数据对象，然后又都请求对已为其他事务封锁的数据对象加锁，从而出现死等待。防止死锁的发生其实就是要破坏产生死锁的条件。预防死锁通常有两种方法：

- 一次封锁法

一次封锁法要求每个事务必须一次将所有要使用的数据全部加锁，否则就不能继续执行。 一次封锁法虽然可以有效地防止死锁的发生，但也存在问题，一次就将以后要用到的全部数据加锁，势必扩大了封锁的范围，从而降低了系统的并发度。

- 顺序封锁法

顺序封锁法是预先对数据对象规定一个封锁顺序，所有事务都按这个顺序实行封锁。 顺序封锁法可以有效地防止死锁，但也同样存在问题。事务的封锁请求可以随着事务的执行而动态地决定，很难事先确定每一个事务要封锁哪些对象，因此也就很难按规定的顺序去施加封锁。 可见，在操作系统中广为采用的预防死锁的策略并不很适合数据库的特点，因此DBMS在解决死锁的问题上普遍采用的是诊断并解除死锁的方法。

#### 死锁的诊断与解除

- 超时法

如果一个事务的等待时间超过了规定的时限，就认为发生了死锁。超时法实现简单，但其不足也很明显。一是有可能误判死锁，事务因为其他原因使等待时间超过时限，系统会误认为发生了死锁。二是时限若设置得太长，死锁发生后不能及时发现。

- 等待图法

事务等待图是一个有向图G=(T,U)。 T为结点的集合，每个结点表示正运行的事务；U为边的集合，每条边表示事务等待的情况。若T1等待T2,则T1、T2之间划一条有向边，从T1指向T2。事务等待图动态地反映了所有事务的等待情况。并发控制子系统周期性地（比如每隔1分钟）检测事务等待图，如果发现图中存在回路，则表示系统中出现了死锁。

数据库特点

- 数据结构化
- 数据的共享性高，冗余度低，易扩展
- 数据独立性高
- 数据由DBMS统一管理和控制

在关系模型中,关系完整性主要是指以下三方面：

- 实体完整性

所谓的实体完整性就是指关系(所谓的关系就是表)的主码不能取空值；
比如学生表的主码通常是取学号为主码

- 参照完整性

是指参照关系中每个元素的外码要么为空(NULL),要么等于被参照关系中某个元素的主码；
比如今天是9月2日是开学日,大学新生刚来报道,在学生表里,有的学生可能还没来得及分配具体的班,所以这些还未来得及分班的学生教务处可以在学生表里的班级属性取空值NULL(空值代表“不确定”),而哪些已分了班的学生就必须取班级表里的某些属性,比如班级类别,即学生属于哪个班.比如取“软件工程”,”计算机技术应用“等等.
参照关系也称为外键表,被参照关系也称为主键表.

- 用户定义的完整性

指对关系中每个属性的取值作一个限制(或称为约束)的具体定义.比如 性别属性只能取”男“或”女“ ,再就是年龄的取值范围,可以取值0-130 ,但不能取负数,因为年龄不可能是负数.