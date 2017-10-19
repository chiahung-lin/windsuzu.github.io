---
title: LeetCode#175 Combine Two Tables - in MySQL
date: 2017-10-19 15:13:44
tags:
- LeetCode
- MySQL
categories:
- LeetCode
- MySQL
---

# 題目
``` 
Table: Person

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.

PersonId 是這個表格的主鍵。
```

```
Table: Address

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.

AddressId 是這個表格的主鍵。
```

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:
FirstName, LastName, City, State

寫一個 SQL 查詢，回傳每一個 Person 的值，以及其對應的 Address 欄位，
格式為 FirstName, LastName, City, State ，
不管有沒有對應的 Address 都要傳回。

---

# 解題

沒什麼難度的 SQL 查詢。

注意的是不管有沒有對應的 Address 都要回傳 Person ，所以要使用 LEFT JOIN 右邊為空時返回 null 即可。

``` sql
SELECT FirstName, LastName, City, State
FROM Person
LEFT JOIN Address ON Person.PersonId = Address.PersonId
```