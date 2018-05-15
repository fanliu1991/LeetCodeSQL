# LeetCodeSQL
LeetCode Database Problems, using MS SQL Server

1.
OFFSET FETCH Clause:

OFFSET { integer_constant | offset_row_count_expression } { ROW | ROWS }
  Specifies the number of rows to skip, before starting to return rows from the query expression. 
  The argument for the OFFSET clause can be an integer or expression that is greater than or equal to zero. 
  You can use ROW and ROWS interchangeably.

FETCH { FIRST|NEXT } <rowcount expression> { ROW|ROWS } ONLY
  Specifies the number of rows to return, after processing the OFFSET clause. 
  The argument for the FETCH clause can be an integer or expression that is greater than or equal to one. 
  You can use ROW and ROWS interchangeably.
  Similarly, FIRST and NEXT can be used interchangeably.

Limitations in Using OFFSET-FETCH:
1. ORDER BY is mandatory to use OFFSET and FETCH clause.
2. OFFSET clause is mandatory with FETCH. You can never use, ORDER BY … FETCH.
3. TOP cannot be combined with OFFSET and FETCH in the same query expression.
4. The OFFSET/FETCH rowcount expression can be any arithmetic, constant, or parameter expression that will return an integer value. 
   The rowcount expression does not support scalar sub-queries.


2. User-defined Functions
use "DECLARE @<variable-name> <variable-type>;" to declare new variable
use "SET @<variable-name> = (@<another-variable-name>) - 1;" to give value to variable


3. 
A subquery can also be found in the SELECT clause. 
These are generally used when you wish to retrieve a calculation using an aggregate function such as the SUM, COUNT, MIN, or MAX function, 
but you do not want the aggregate function to apply to the main query.

For example:

SELECT e1.last_name, e1.first_name,
  (SELECT MAX(salary)
   FROM employees e2
   WHERE e1.employee_id = e2.employee_id) AS subquery2
FROM employees e1;


4. Four ranking functions used in the same query
The following shows the four ranking functions used in the same query. 

For function specific examples, see each ranking function.

SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS Rank  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS Quartile  
    ,s.SalesYTD  
    ,a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  


Here is the result set.

+-----------+------------------+------------+------+------------+----------+-------------+------------+
| FirstName |     LastName     | Row Number | Rank | Dense Rank | Quartile |  SalesYTD   | PostalCode |
+-----------+------------------+------------+------+------------+----------+-------------+------------+
| Michael	  | Blythe	         | 1	        | 1	   | 1	        | 1        | 4557045.0459| 98027      |
| Linda     | Mitchell         | 2          | 1    | 1          | 1        | 5200475.2313| 98027      |
| Jillian   | Carson           | 3          | 1    | 1          | 1        | 3857163.6332| 98027      |
| Garrett   | Vargas           | 4          | 1    | 1          | 1        | 1764938.9859| 98027      |
| Tsvi      | Reiter           | 5          | 1    | 1          | 2        | 2811012.7151| 98027      |
| Shu       | Ito              | 6          | 6    | 2          | 2        | 3018725.4858| 98055      |
| José      | Saraiva          | 7          | 6    | 2          | 2        | 3189356.2465| 98055      |
| David     | Campbell         | 8          | 6    | 2          | 3        | 3587378.4257| 98055      |
| Tete      | Mensa-Annan      | 9          | 6    | 2          | 3        | 1931620.1835| 98055      |
| Lynn      | Tsoflias         | 10         | 6    | 2          | 3        | 1758385.926 | 98055      |
| Rachel    | Valdez           | 11         | 6    | 2          | 4        | 2241204.0424| 98055      |
| Jae       | Pak              | 12         | 6    | 2          | 4        | 5015682.3752| 98055      |
| Ranjit    | Varkey Chudukatil| 13         | 6    | 2          | 4        | 3827950.238 | 98055      |
+-----------+------------------+------------+------+------------+----------+-------------+------------+

