---
layout: post
title:  SQL优化
date:   2019-09-21 020:08:00 +0800
categories: DB
tag: 笔记
---	

* content
{:toc}

SQL-优化关键点 
====================================

 1. 避免全表扫描
 2. 避免索引失效
 3. 避免排序，若不能避免，尽量选择索引排序
 4. 避免查询不必要的字段
 5. 避免临时表的创建，删除


插入数据时
------------------------------------

 1. 导入大量数据，可以考虑先关闭索引，插入数据完成后打开索引
	alert table user disable keys;// disable all key
	alert table user enable keys;// enable all keys
  对于Innodb类型的表， 由于Innodb的表示根据主键的顺序保存的，所以将导入的数据按照主键的顺序，可以提高效率
 
   再导入数据前关闭唯一性校验也是可以提高效率 set unique_checks = 0
   关闭自动提交 set auto-commit = 0 采用手动提交也可以提高效率
  
 2. 优化insert语句
	如果同时插入多行，采用多个值表更好，
	insert into test value （1,2）(1,3)(...);

排序 Order By
------------------------------------------------------------------------

  尽量减少额外的排序，通过索引返回有效数据
	1. 通过有序索引顺序扫描直接返回有序数据，
	select customer_id from customer order by store_id;
 	2. 通过返回数据进行排序， 
	select * from customer order by store_id;

分组优化group by
------------------------------------------------------------------------

	默认情况下group by 对字段分组的时候会排序，
	如果在分组的时候不需要排序，最好关掉排序命令， order by null 
	selec name ,sum(money) from user group by name order by null;

优化嵌套查询
------------------------------------------------------------------------

	某些子查询可以通过join来代替， join不需要在内存中创建一个临时表来存储数据
	select * from customer where customer_id not in (select customer_id from payment);
	可优化成 
	select * from customer_is a left join payment b on a.customer_id = b.customer_id where b.customer_id is null;

优化or条件
------------------------------------------------------------------------
	1. 对于单独的两个索引
	select * from sales whrere id =2 or year =1998;
	这另个索引都被使用了，查询的时候是分别对两个条件进行查询，然后union两个结果
	2. 如果对复合索引（如果id year 是复合索引），那么就没有使用索引，而是采用了全文扫描


优化分页查询
------------------------------------------------------------------------

使用sql提示
------------------------------------------------------------------------

查询的一些注意事项
------------------------------------
	1. 慎用模糊查询 使用like 两边加 "%"会导致索引失效，如果左边没有%则索引不会失效
	2. 尽量不要使用select * 
	3. 不要在查询条件where后面对字段做函数处理
	4. 优先使用union all 避免使用union
		1. UNION 会将各查询的子集记录作比较，故比起UNION ALL ,通常速度都会满上许多，一般来说，如果使用UNION ALL 能满足需求的话，务必使用UNION ALL, 
	5. 使用not exsit 代替 not in
		如果语句使用了 not in 那么内外表都会进行全表扫描，没有用到索引，儿not exist 的子查询依然能用到表上的索引
	6. in 和 exist 的区别
		1. in 是把外表和内表做hash连接， 而exist是对外表做loop循环，每次loop循环再对表内进行查询。因此，in 用到的 是外表的索引。 exists 用到的是内表的索引。
		如果两个表大小相当那么用 in 和 exsit 差别不大
		如果两个中的一个较小，一个是大表，则子查询表大的用exists 子查询表小的用in  
	7. 避免在索引上做如下操作，当在索引列上使用如上操作时，索引将会失效造成全表扫描
		1. 避免在索引字段上使用 <> ！=
		2. 避免在索引列上使用 is null ， is not null
		3. 避免在索引列上出现数据类型转换（如字段是string 传入的参数确实int）