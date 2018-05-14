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
