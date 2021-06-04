#### limit N

**N** is any number starting from 0, putting 0 as the limit does not return any records in the query.  Putting a number say 5 will return five records.

If the records in the specified table are less than N, then all the records from the queried table are returned in the result set.

e.g.,

```mysql
SELECT *  FROM members LIMIT 5;
```

Using ***offset*** in the LIMIT query

The OFF SET value allows us to specify which row to start from retrieving data

```mysql
SELECT * FROM members LIMIT 1, 2;
### offset = 1, i.e., start from 2
### limit = 2
```

The script shown above gets data starting the second row and limits the results to 2.

---

#### in() function

The function returns 1 if expression is equal to any of the values in the IN list, otherwise, returns 0.

```mysql
SELECT 
    column1,column2,...
FROM
    table_name
WHERE 
    (expr|column_1) IN ('value1','value2',...);
```



```mysql
mysql> SELECT 10 IN(15,10,25);
+-----------------+
| 10 IN(15,10,25) |
+-----------------+
|               1 | 
+-----------------+
1 row in set (0.00 sec)
```

---

#### IF(*condition*, *value_if_true*, *value_if_false*)

```mysql
SELECT IF(500<1000, 5, 10);
```



---

#### ROUND(*number*, *decimals*)

Parameters:

*number*:  Required. The number to be rounded

*decimals*: Optional. The number of decimal places to round *number* to. If omitted, it returns the integer (no decimals)

```mysql
SELECT ROUND(135.375, 2); // 135.38
```



#### COUNT(*expression*)

Parameters:

*expression*: Required. A field or a string value

```mysql
SELECT COUNT(ProductID) AS NumberOfProducts FROM Products; // 77
```



---

##### dense_rank()

```mysql
1875.
# Write your MySQL query statement below

select e1.employee_id, e1.name, e1.salary, e2.team_id
from Employees as e1
inner join (
select salary, dense_rank() over (
    order by salary
) as team_id
from Employees
group by salary
having count(distinct employee_id) > 1
# {"headers": ["salary", "team_id"], "values": [[3000, 1], [7400, 2]]}
) as e2
on e1.salary = e2.salary
order by e2.team_id, e1.employee_id
```

