---
title: SQL
date: 2019-11-12 14:32:03
tags:
---
### 数据库
### 关系型（二维表格模型）
MySql, Orcale, SqlServer, Access
### 非关系型
MongoDB Redis
### 表 Table
结构化清单
模型（Schema）数据库和表布局信息
### 列 Column
表中的一个字段 对应数据类型
### 行 Row
一条记录
### 主键 Primary Key
一（多）列唯一值 不能修改更新重用

## 检索
### SELECT语句
SELECT * FROM 表;
SELECT 列1, 列2, 列3 FROM 表;
SELECT
&emsp;DISTINCT 区别值
&emsp;TOP 5 最多返回5行
FROM 表
&emsp;FETCH FIRST 5 ROW ONLY
&emsp;WHERE ROWNUM（行计数器） <=5
&emsp;LIMIT 5
&emsp;LIMIT 5 OFFSET 6 从第6行开始
&emsp;WHERE 一列条件
&emsp;&emsp;BETWEEN AND
&emsp;&emsp;IS NULL 检查空值
&emsp;ORDER BY 列
&emsp;最后一条 可多列 DESC降序
\#注释
