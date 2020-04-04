# 1. 窗口函数

| 函数           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| ROW_NUMBER()   | 从1开始，按照顺序，生成分组内记录的序列，比如，按照pv降序排列，生成分组内每天的pv名次，ROW_NUMBER()的应用 场景非常多，再比如，获取分组内排序第一的记录，获取一个session中的第一条refer等 |
| RANK()         | 生成数据项在分组中的排名，排名相等会在名次中留下空位         |
| DENSE_RANK()   | 生成数据项在分组中的排名，排名相等会在名次中不会留下空位     |
| CUME_DIST()    | 小于等于当前值的行数除以分组内总行数。比如，统计小于等于当前薪水的人数所占总人数的比例 |
| PERCENT_RANK() | 分组内当前行的RANK值-1/分组内 总行数-1                       |
| NTILE(n)       | 用于将分组数据按照顺序切分成n片，返回当前切片值，如果切片不均匀，默认增加第一个切片的分布。NTILE不支持ROWS BETWEEN,比如NTILE(2) OVER(PARTITION BY cookieid ORDER BY createtime ROWS BETWEEN 3 PERCEDING AND CURRENT ROW) |

Hive窗口函数可以计算一定范围内、一定值域内、或者一段时间内的**累积和以及移动平均值**等；可以结合聚集函数SUM() 、AVG()等使用；可以结合FIRST_VALUE() 和LAST_VALUE()，返回窗口的第一个和最后一个值。



- 如果只使用PARTITION BY子句,未指定ORDER BY的话,我们的聚合是分组内的聚合.
- 使用了ORDER BY子句,未使用window子句的情况下,默认从起点到当前行.
  window子句：
- PRECEDING：往前
- FOLLOWING：往后
- CURRENT ROW：当前行
- UNBOUNDED：起点，UNBOUNDED PRECEDING 表示从前面的起点， UNBOUNDED FOLLOWING：表示到后面的终点

## 1.1 计算累计和

统计1-12月的累积和，即1月为1月份的值，2月为1、2月份值的和，3月为123月份的和，12月为1-12月份值的和。
关键字解析：

- SUM(SUM(amount)) 内部的SUM(amount)为需要累加的值；
- ORDER BY month 按月份对查询读取的记录进行排序，就是窗口范围内的排序；
- ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW 定义起点和终点，UNBOUNDED
- PRECEDING 为起点，表明从第一行开始, CURRENT ROW为默认值，就是这一句等价于：
- ROWS UNBOUNDED PRECEDING
- PRECEDING：在前 N 行的意思。
- FOLLOWING：在后 N 行的意思。

### 1.1.1 计算所有月份的累计和

```
  select pt_month, 
         sum(amount) pay_amount,
         sum(sum(amount))over(order by pt_month) cumulative_amount
    from data_chushou_pay_info
   where pt_month between '2017-01' and '2017-12' 
     and state=0
group by pt_month;

  select pt_month,
         sum(amount) pay_amount,
         sum(sum(amount))over(order by pt_month ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) cumulative_amount
    from data_chushou_pay_info
   where pt_month between '2017-01' and '2017-12' 
     and state = 0
group by pt_month;
```

### 1.1.2 计算前3个月和本月共4个月的累积和

```
  select pt_month,
         sum(amount) pay_amount,
         -- 从当前行开始，再往前数3行
         sum(sum(amount))over(order by pt_month ROWS BETWEEN 3 PRECEDING AND CURRENT ROW) cumulative_amount
    from data_chushou_pay_info
   where pt_month between '2017-01' and '2017-12' and state=0
group by pt_month;

  select pt_month,
         sum(amount) pay_amount,
         sum(sum(amount))over(order by pt_month ROWS 3 PRECEDING) cumulative_amount
    from data_chushou_pay_info
   where pt_month between '2017-01' and '2017-12' 
     and state = 0
group by pt_month;
```

### 1.1.3 计算前1月后1月和本月共3个月的累积和

```
  select pt_month,
         sum(amount) pay_amount,
         sum(sum(amount))over(order by pt_month ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) cumulative_amount  
    from data_chushou_pay_info  
   where pt_month between '2017-01' and '2017-12' 
     and state = 0  
group by pt_month;
```

## 1.2 计算平均值

### 1.2.1 计算前1月后1月和本月共3个月各月总值的平均值

```
  select pt_month,
         sum(amount) pay_amount,
         avg(sum(amount))over(order by pt_month ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) average_amount  
    from data_chushou_pay_info  
   where pt_month between '2017-01' and '2017-12' 
     and state = 0  
group by pt_month;
```

### 1.2.2 计算前3个月和本月共4个月各月总值的平均值

```
  select pt_month,
         sum(amount) pay_amount,
         avg(sum(amount))over(order by pt_month ROWS BETWEEN 3 PRECEDING AND CURRENT ROW) cumulative_amount  
    from data_chushou_pay_info  
   where pt_month between '2017-01' and '2017-12' 
     and state = 0  
group by pt_month;
```

## 1.3 计算窗体第一条和最后一条的值

```
  select pt_month,
         sum(amount) pay_amount,
         first_value(sum(amount))over(order by pt_month ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) first_amount,
         last_value(sum(amount))over(order by pt_month ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) last_amount  
    from data_chushou_pay_info  
   where pt_month between '2017-01' and '2017-12' 
     and state = 0  
group by pt_month;
```

## 1.4 ROW_NUMBER

在做row_number() over() 排序时，排序要严格确认顺序，不然有相同顺序条件，多次执行结果就可能不一致的(相同条件会随机取)

# 2. 分析函数

# 3. 视图

# 4. 常见CASES

## 4.1 实现一个字段包含另一个字段的查询

```
select * 
  from data_chushou_pay_info 
 where name1 like concat('%', name2, '%');
```

## 4.2 分组排序 取top N

```
select t1.*
  from ( select 品牌,
                渠道,
                档期,
                count/sum/其它() as num row_number() over (partition by 品牌,渠道,档期 
                                                          order by num desc ) rank
           from table_1
          where 品牌,渠道 限制条件
       group by 品牌,渠道,档期)
 where t1.rank <= 10
```

## 4.3 聚合函数与COALESCE和IF组合使用

> COALESCE(arg1, arg2, arg3…)：遇到非null参数即返回该值

```
SELECT SUM(COALESCE(sex_age.age, 0)) AS age_sum, 
       SUM(IF(sex_age.sex='Female', sex_age.age, 0)) AS female_age_sum 
  FROM employee;
```

![img](http://chenson.cc/2019/06/17/Hive%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E5%B0%8F%E7%BB%93/2019-06-17-Hive%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E5%B0%8F%E7%BB%93/SouthEast.png)

## 4.4 聚合函数与DISTINCT关键词组合使用

```
SELECT COUNT(DISTINCT sex_age.sex) AS sex_uni_cnt, 
       COUNT(DISTINCT name) AS name_uni_cnt 
  FROM employee;
```

![img](http://chenson.cc/2019/06/17/Hive%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E5%B0%8F%E7%BB%93/2019-06-17-Hive%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E5%B0%8F%E7%BB%93/SouthEast.png)

**注：如果COUNT和DISTINCT连用，Hive将忽略对reducer个数的设置（如：set mapred.reduce.tasks=20;）, 仅会有一个reducer！此时reduce将成为瓶颈，这时我们可以使用子查询的方式解决该问题。**

```
SELECT COUNT(*) AS sex_uni_cnt 
  FROM (SELECT DISTINCT sex_age.sex FROM employee) a;
```

## 4.5 采样

当数据集非常大的时候，我们需要找一个子集来加快数据分析。此时我们需要数据采集工具以获得需要的子集。在此可以使用三种方式获得采样数据：random sampling， bucket sampling， block sampling.

### 4.5.1 Random Sampling

使用RAND()函数和LIMIT关键字来获取样例数据。使用DISTRIBUTE和SORT关键字来保证数据是随机分散到mapper和reducer的。ORDER BY RAND()语句可以获得同样的效果，但是性能没这么高

```
SELECT * 
  FROM <Table_Name> DISTRIBUTE BY RAND() SORT BY RAND()  
 LIMIT <N rows to sample>;
```

### 4.5.2 Bucket Sampling

该方式是最佳化采样bucket表。RAND()函数也可以用来采样整行。如果采样列同时使用了CLUSTERED BY，使用TABLESAMPLE语句会更有效率。

```
SELECT * 
  FROM <Table_Name>  
  TABLESAMPLE(BUCKET <specified bucket number to sample> OUT OF <total number of buckets> ON [colname|RAND()]) table_alias;
```

### 4.5.3 Block Sampling

## 4.6 GROUPING SETS

```
-- /***** CASE-1 *****/
    SELECT a, b, SUM( c ) 
      FROM tab1 
  GROUP BY a, b GROUPING SETS (a,b)
    -- 相当于
    SELECT a, b, SUM(c) 
      FROM tab1 
  GROUP BY a, b
  
-- /***** CASE-2 *****/  
    SELECT a, b, SUM( c ) 
      FROM tab1 
  GROUP BY a, b GROUPING SETS ((a,b), a)
    -- 相当于
    SELECT a, b, SUM( c ) 
      FROM tab1 
  GROUP BY a, b
     UNION
    SELECT a, null, SUM( c ) 
      FROM tab1 
  GROUP BY a
  
-- /***** CASE-3 *****/  
    SELECT a, b, SUM( c ) 
      FROM tab1 
  GROUP BY a, b GROUPING SETS (a,b)
      -- 相当于
    SELECT a, null, SUM( c ) 
      FROM tab1 
  GROUP BY a
     UNION
    SELECT null, b, SUM( c ) 
      FROM tab1 
  GROUP BY b
```

注：似乎对Hive的版本有要求，具体版本号有点记不清了。

# 5. 常见优化

## 5.1 基于条件的LEFT OUTER JOIN优化

左连接时，左表中出现的JOIN字段都保留，右表没有连接上的都为空。对于带WHERE条件的JOIN语句，例如：

```
SELECT a.val, 
       b.val 
  FROM a 
  LEFT OUTER JOIN b 
    ON (a.key = b.key)
 WHERE a.ds = '2009-07-07' 
   AND b.ds = '2009-07-07'
```

执行顺序是，首先完成2表JOIN，然后再通过WHERE条件进行过滤，这样在JOIN过程中可能会输出大量结果，再对这些结果进行过滤，比较耗时。可以进行优化，将WHERE条件放在ON后，例如

```
SELECT a.val, 
       b.val 
  FROM a 
  LEFT OUTER JOIN b
    ON a.key = b.key 
   AND b.ds = '2009-07-07' 
   AND a.ds = '2009-07-07'
   
-- 用子查询优化
-- 将where条件放到子查询中，查询效率将会提高很多
SELECT a.val,
       b.val
  FROM (SELECt * FROM a WHERE a.ds = '2009-07-07')
  LEFT OUTER JOIN (SELECT * FROM b WHERE b.ds = '2009-07-07')
    ON a.key = b.key
```

**多用子查询，多用where，然后再join**。

如果先join，就全表扫描，然后最后where最后筛选，比较耗时。

如果用子查询，就可以利用where过滤不相关的字段，不但增加了map 数量，还减少了数据量。

尽量尽早地过滤数据，减少每个阶段的数据量,对于分区表要加分区，同时只选择需要使用到的字段.

**小表要注意放在join的左边**（有的公司很多都小表放在join的右边）否则会引起磁盘和内存的大量消耗。hive会将join前面的表数据装载内存,所以较小的一个表在较大的表之前,减少内存资源的消耗

## 5.2 左半连接（LEFT SEMI JOIN）

**左半连接实现了类似IN/EXISTS的查询语义**，使用关系数据库子查询的方式实现查询SQL，例如：

```
SELECT a.key, 
       a.value 
  FROM a 
 WHERE a.key IN (SELECT b.key FROM b);
```

使用Hive对应于如下语句：

```
SELECT a.key, 
       a.val 
  FROM a 
  LEFT SEMI JOIN b ON (a.key = b.key)
```

需要注意的是，在LEFT SEMI JOIN中，表b只能出现在ON子句后面，不能够出现在SELECT和WHERE子句中。
关于子查询，这里提一下，Hive支持情况如下：

- 在0.12版本，只支持FROM子句中的子查询；
- 在0.13版本，也支持WHERE子句中的子查询。

# 6. 常见问题

## 6.1 数据倾斜

### 6.1.1 JOIN的KEY倾斜

- 空值 [[Hive\]Hive数据倾斜（大表join大表）](https://blog.csdn.net/yeweiouyang/article/details/45665727)
- **事实上“把小表放在前面做关联可以提高效率”这种说法是错误的。正确的说法应该是“把重复关联键少的表放在join前面做关联可以提高join的效率。”**【缺确认】[Hive中小表与大表关联(join)的性能分析](https://blog.csdn.net/xiewenbo/article/details/24886689)

# 7. References

- [转发链接]([http://chenson.cc/2019/06/17/Hive%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E5%B0%8F%E7%BB%93/#&gid=1&pid=1](http://chenson.cc/2019/06/17/Hive常用函数小结/#&gid=1&pid=1))

- [Hive分析函数和窗口函数](https://www.jianshu.com/p/acc8b158daef)
- [Hive JOIN使用详解](http://shiyanjun.cn/archives/588.html)
- [hive子查询sql效率优化](https://blog.csdn.net/qq_29232943/article/details/79644614)
- [hive 查询性能优化总结](https://www.jianshu.com/p/6970c47eec5c)
- [hive-where和having的区别](https://blog.csdn.net/high2011/article/details/82686858)
- [WHERE和HAVING的区别?](https://blog.csdn.net/J_Cxn/article/details/79455595)
- [Hive聚合函数及采样函数详解](https://blog.csdn.net/yhao2014/article/details/46340471)

