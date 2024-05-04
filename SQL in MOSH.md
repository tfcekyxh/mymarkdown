# SQL

## TABLE tricks

| create a Copy of a table |
| ------------------------ |
| **the ROLLUP operation** |

`CREATE TABLE a AS SELCET * FROM orders`

```sql
SELECT 	customer_id,
		SUM(total_sales)
FROM invoices
GROUP BY client,states,city WITH ROLLUP -- only mySQL
```



## writing Complex Query

| Find clients without invoices                             |                             |
| --------------------------------------------------------- | --------------------------- |
| **Select invoices larger than all invoices of client  3** | (MAX) / (> ALL)             |
| **Select clients with at least two invoices**             | (IN)/ (= ANY)               |
| **Select ......**                                         | Correlated Query            |
| **Select clients that have an invoice**                   | EXIST                       |
| **Find the products that have never been ordered**        | EXIST                       |
| **Make a report includes total, average, difference**     | Subqueries in SELECT clause |



## SQL functions

| Numeric functions                                            |
| ------------------------------------------------------------ |
| **String functions**                                         |
| **Date functions**                                           |
| **DATE_FORMAT(NOW(),'%y')** / **TIME_FORMAT(NOW(),'%H:%i %p')** |
| **IFNULL** / **COALESCE**                                    |
| **IF**                                                       |
| **CASE ... WHEN  ... THEN**                                  |



## Updatable views

| **CREATE OR REPLACE VIEW** |
| -------------------------- |
| **WITH CHECK OPTION**      |



## Stored Procedure

https://www.w3schools.com/SQL/sql_stored_procedures.asp

[https://www.sqltutorial.net/create-function.html](https://www.sqltutorial.net/create-function.html)

| `MYSQL` NEEDS DELIMILATER, `SQL SERVER` doesn't;             |
| ------------------------------------------------------------ |
| **`MYSQL` needn't '@' front of parameters, otherwise for SQL SERVER** |
| **Parameter with  DEFAULT value**                            |
| **Parameter Validation** ( less )                            |
| **Output parameters**                                        |
| **Variables**                                                |
| **Functions**                                                |

