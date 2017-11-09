---
title: LeetCode#183 Customers Who Never Order - in MySQL
date: 2017-11-03 11:07:43
tags:
- LeetCode
- MySQL
categories:
- LeetCode
- MySQL
---

# 題目

Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.

給你兩個表格代表客人和點單記錄 (Customers & Orders) ，寫出一個 SQL Query ，找出哪些客人沒有點過任何東西。

``` swift
Table: Customers.

+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+

Table: Orders.

+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
```

---

# 範例

``` swift
Using the above tables as example, return the following:

+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
```

依照上方兩個表格的範例，可以查出 Henry 和 Max 沒有買過東西。

---

# 解題

有三種解法:

## NOT EXISTS

利用 NOT EXISTS 排除 C.Id = O.CustomerId 的查詢，負負得正，就是沒有下訂單的客人。

``` sql
SELECT C.Name
FROM Customers C
WHERE NOT EXISTS
(SELECT Id
FROM Orders O
WHERE C.Id = O.CustomerId)
```

## NOT IN

類似 NOT EXISTS ，但直接利用 C.Id 查出不存在 O.CustomerId 的欄位。

``` sql
SELECT C.Name
FROM Customers C
WHERE C.Id NOT IN
(SELECT O.CustomerId
FROM Orders O)
```

## LEFT JOIN

LEFT JOIN 不管任何事都會把左邊印出，找出 C.Id = O.CustomerId ，如果沒有下過訂單，右邊就會為 NULL ，把這些右邊為 NULL 的欄位擷取出來即可。

``` sql
SELECT C.Name
FROM Customers C
LEFT JOIN Orders O on C.Id = O.CustomerId
WHERE O.CustomerId is NULL
```


