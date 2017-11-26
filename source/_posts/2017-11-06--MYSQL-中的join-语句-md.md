---
title: MYSQL-中的join-语句.md
tags: ['MYSQL']
date: 2017-11-06 17:30:21
categories: DB
---
1, left join 可以将两个表进行合并，左表的数据完全保留，右表的数据在on条件符合的情况下进行筛选后保留。
select P.FirstName, P.LastName, A.City, A.State from Person as P LEFT JOIN Address as A on P.PersonId = A.PersonID
select 左右表数据 from 左表 as 简名 LEFT JOIN 右表 as 简名 on 过滤条件 
 同理，right join 可以将右表所有数据显示，将左表过滤显示。
<!-- more -->

如下文章用集合来表示，join的数据结构。
http://www.cnblogs.com/sunjie9606/p/4167190.html

inner join 表示交集，
full join 表示合集
left join 表示左全集附加右过滤条件
right join 表示右
outer join 包括full left right join

cross join表示笛卡尔积，表示所有可能性的组合情况
