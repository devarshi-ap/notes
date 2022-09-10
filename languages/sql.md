# SQL

**SQL - Structured Query Language**

Allows users to query, manipulate, and transform data from a relational database.

Most commonly, a data model is designed first, then data is deconstructed by the process of "normalization". This aims to turn your data in a basic form like into separate tables. E.g. one table for customers and one for orders

### RDBMS

SQL is a language which has many **Relational Database Management Systems (RDBMS)** that all support the common SQL language standard but differ in the additional features and storage types it supports:

* SQLite, MySQL, Postgres, Oracle, Microsoft (MS) SQL Server

_**Table**_ - collection of related data entries; it consists of **columns** and **rows**

* **fixed # of labelled columns** (a.k.a. attributes/properties/fields)
* **any # of rows of data** (a.k.a. record) (individual entries that exist on a table)
* Each table is identified by a name (ie. 'Cars')

## SQL Statements

* SQL keywords are NOT case sensitive: `select` === `SELECT`
* Each statement ends in a ; (like Java)

|     SQL COMMAND     | Description                   |
| :-----------------: | ----------------------------- |
|      **SELECT**     | selects data from db          |
|      **UPDATE**     | updates data in db            |
|      **DELETE**     | deletes data from db          |
|   **INSERT INTO**   | inserts new data into db      |
| **CREATE DATABASE** | creates new db                |
|  **ALTER DATABASE** | modifies db                   |
|   **CREATE TABLE**  | creates new table             |
|   **ALTER TABLE**   | modifies table                |
|    **DROP TABLE**   | deletes table                 |
|   **CREATE INDEX**  | creates an index (search key) |
|    **DROP INDEX**   | deletes an index              |

### > SELECT

* colloquially refered to as _queries_, which in itself is just a statement which declares what data we're looking for, where to find it in the db.

```sql
/* SYNTAX */
select <col_names> from <table_name>;

/* ex. Cars table: */
select Company, Price, Color from Cars

/* SELECT ALL */
select * from Cars;
```

### > SELECT DISTINCT

* gets distinct values in specified column(s) of a table

```sql
/*
ex. Car Garage table --> gets Company, but no-repeat values
*/
select distinct Company from Garage;
```

### > WHERE

* used to filter rows that are retrieved from table
* can be paired with _select / update / delete_

```sql
/* Syntax */
select * from Garage
where <condition>;
```

* The is built using operators (ex. follows above):

| Operator |                   Description                   | Ex.                                                                         |
| :------: | :---------------------------------------------: | --------------------------------------------------------------------------- |
|     =    |               equal ('abc' \| 123)              | `where Company='BMW'`                                                       |
|     >    |                   greater than                  | `where Price>50000`                                                         |
|     <    |                    less than                    | `where Price<50000`                                                         |
|    >=    |               greater than or = to              | `where Price>=50000`                                                        |
|    <=    |                less than or = to                | `where Price<=50000`                                                        |
|    <>    |             not equal ('abc' \| 123)            | `where Color<>'Blue'`                                                       |
|  BETWEEN |             between a certain range             | `where Price BETWEEN 10000 AND 20000`                                       |
|   LIKE   |               search for a pattern              | `where Company LIKE 's%'` (starts with s)                                   |
|     %    | match sequence of chars (only w/ LIKE/NOT LIKE) | `where col_name LIKE '%AT%'` matches = ("AT", "ATTIC", "CAT", "BATS", ... ) |
|     -    |  used anywhere in a str to match a single char  | `where col_name LIKE 'AN_'` matches=("AND", but not "AN")                   |
|    IN    |     specify multiple possible values for col    | `where Company IN ('BMW', 'Tesla')`                                         |

* note: text columns must use `'single-quotes'` and numeric columns should not.
* [Wildcard Characters for **LIKE**](https://www.w3schools.com/sql/sql\_wildcards.asp)

You can chain multiple conditions in a WHERE clause using logical operators:

*   **AND**

    ```sql
    /* displays a row from col1 if ALL 3 conditions are true */
    select col1
    from table_name
    where cond1 AND cond2 AND cond3;
    ```
*   **OR**

    ```sql
    /* displays a row from col1 if ANY of the 3 conditions are true */
    select col1
    from table_name
    where cond1 OR cond2 OR cond3;
    ```
*   **NOT**

    ```sql
    /* displays a row from col1 if cond1 is NOT TRUE  but the rest are */
    select col1
    from table_name
    where NOT cond1 AND cond2 AND cond3;
    ```

Now, we can construct more complex clauses:

```sql
between 1 and 10
not between 1.5 and 10.5
in (2, 4, 6, 8, 10)
not in (1, 3, 5, 7, 9)
```

### > ORDER BY

* sorts the result-rows in **ASC** (default) or **DESC** order

```sql
/* all cars sorted by Price in ASC order */
select * from Garage
order by Price ASC;
```

*   You can sort multiple columns too:

    ```sql
    /*
    orders by Price (asc) but if some rows have the same Price, it orders them by Name (desc)
    */
    select * from Garage
    order by Price ASC, Name DESC
    ```
*   clauses **LIMIT** and **OFFSET** are commonly used with the **ORDER BY** clause.

    ```sql
    /*
    limit - reduce the number of rows to return
    offset - where to begin counting # rows from
    */
    SELECT a_column, another_column, …
    FROM mytable
    WHERE condition
    ORDER BY column ASC/DESC
    LIMIT num_limit OFFSET num_offset;
    ```

***

## Multi-Table Queries with JOINs

Up to now, we've been working with a single table, but entity data in the real world is often broken down into pieces and stored across multiple orthogonal tables using a process known as _**normalization**_

_**Database Normalization**_

* every entity is organized into its own table
* process of organizing data in a database
* This includes creating tables and establishing relationships between those tables

Tables that share info about a single entity need to have a _**primary key**_ that identifies _that_ entity _uniquely_ across the database; this is usually an _**auto-incrementing integer**_ (but could be string/hash/...)

### $ JOINs

* used to combine rows from 2 or more tables, based on a related column b/n them.



![How to Learn SQL JOINs | LearnSQL.com](https://learnsql.com/blog/learn-and-practice-sql-joins/2.png)

## > (INNER) JOIN

* Returns records that have matching values in both tables

![Gif of how inner join iterates through the tables](https://dataschool.com/assets/images/how-to-teach-people-sql/innerJoin/innerJoin\_3.gif)

* matches rows from the first table and the second table which have the same key (as defined by the **ON** constraint) to create a result row with the combined columns from both tables.
*   You can write either _**`INNER JOIN`**_ or _**`JOIN`**_

    ```sql
    SELECT col, another_table_col, … FROM mytable
    INNER JOIN another_table 
        ON mytable.id = another_table.id
    ```

## > LEFT (OUTER) JOIN

* Returns all records from the left table, and the matched records from the right table

![Shows the Left join adding matches between the left and right table to the result table](https://dataschool.com/assets/images/how-to-teach-people-sql/leftJoin/leftJoin\_1.gif)

*   The result is **NULL** in the consecutive tables when there is no match

    ```sql
    SELECT col, another_table_col, … FROM mytable
    LEFT JOIN another_table 
        ON mytable.id = another_table.id
    ```

## > RIGHT (OUTER) JOIN

* Returns all records from the right table, and the matched records from the left table

![Shows how a right join iterates through the tables](https://dataschool.com/assets/images/how-to-teach-people-sql/leftJoin/leftJoin\_3.gif)

*   The result is **NULL** in the consecutive tables when there is no match

    ```sql
    SELECT col, another_table_col, … FROM mytable
    RIGHT JOIN another_table 
        ON mytable.id = another_table.id
    ```

## > FULL (OUTER) JOIN

* simply means that rows from both tables are kept, regardless of whether a matching row exists in the other table

![gif showing part one of a full outer join: the left join](https://dataschool.com/assets/images/how-to-teach-people-sql/fullOuter/fullOuter\_1.gif)

```sql
SELECT col, another_table_col, … FROM mytable
FULL JOIN another_table 
    ON mytable.id = another_table.id
```

***

## NULLs

* It's always good to reduce the possibility of _**`NULL`**_ values in databases bc they require special attention when constructing queries, constraints and when processing the results.
* Alternatives to _**NULL**_ values include:
  * 0 (for numerical data)
  * '' (for text data)
* But if your database needs to store incomplete data, then _**`NULL`**_ values can be appropriate if the default values will skew later analysis

```sql
/* Gets employees whose building is null */
SELECT * FROM employees
WHERE Building IS NULL;

/* optionally: not null */
WHERE Building IS NOT NULL;
```

***

## Queries with expressions

you can also use _expressions_ to write more complex logic on column values in a query.

The use of expressions save time but can also make the query harder to read; so it's recommended that you use a _descriptive alias_ _**`AS`**_ keyword adfter the SELECT part of the query.

```sql
/* syntax */
SELECT col_expression AS expr_description, …
FROM mytable;

/* ex. */
SELECT speed / 2.0 AS half_speed
FROM physics_data

/*
In addition to expressions, regular columns and even tables can also have aliases.
*/
SELECT column AS better_column_name, …
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
  ON mywidgets.id = widget_sales.widget_id;
```

***

## Queries with aggregates

_**Aggregate Function**_ - SQL performs a calculation on multiple values and returns a single value

SQL provides many aggregate functions:

!\[Screen Shot 2022-07-02 at 4.54.32 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-07-02 at 4.54.32 PM.png)

_**GROUPED AGGR. FUNCTIONS**_

* In addition to aggregating across all the rows, you can instead apply the aggregate functions to individual groups of data within that group
*   This would then create as many results as there are unique groups defined as by the _**`GROUP BY`**_ clause, which groups rows that have the same values into summary rows.

    ```sql
    SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
    FROM mytable
    WHERE constraint_expression
    GROUP BY column;
    ```

Note:

*   if you want to add a **WHERE** clause after a **GROUP BY** clause which is already preceded by a **WHERE** clause, use the **HAVING** clause (treat exactly like WHERE):

    ```sql
    where condition1
    group by col1
    having group_condition
    ```

***

## Order of execution of a Query

(SQL BEDMAS)

1. _**`FROM`**_ , _**`JOIN`**_
2. _**`WHERE`**_
3. _**`GROUP BY`**_
4. _**`HAVING`**_
5. _**`SELECT`**_
6. _**`DISTINCT`**_
7. _**`ORDER BY`**_
8. _**`LIMIT / OFFSET`**_

***

## Inserting Rows

_**SCHEMAS**_ - describes the structure of each table, and the datatypes that each column of the table can contain. (think: mongoose schema)

### > INSERT INTO

* Used to insert new rows in a table. Can be written 2 ways:

1.  Specify **both** the _**column names**_ and the _**values**_ to be inserted

    ```sql
    /* syntax */
    INSERT INTO table_name (col1, col2, ...)
    VALUES (value1, value2, ...); 

    /* ex. */
    INSERT INTO Cars (brand, color, price)
    VALUES ('Porsche',  'Red', 90000);
    ```
2.  If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query. However, make sure the **order of the values** is in the same **order as the columns in the table**.

    ```sql
    /* syntax */
    INSERT INTO table_name
    VALUES (value1, value2, ...);

    /* ex. */
    INSERT INTO Cars
    VALUES
    	('Porsche',  'Red', 90000),
    	('Nissan',  'Navy', 75000);
    ```

Note: you don't need to insert the ID field as it's an **auto-incrementing field** and will be generated automatically when a new row is inserted into the table.

***

## Updating Rows

### > UPDATE (+ SET)

* used to modify the existing records in a table
* Similar to the _**`INSERT`**_ statement, you have to specify exactly which table, columns, and rows to update.
* the data you are updating has to follow the schema of those columns.

```sql
/* syntax */
UPDATE mytable
SET column_1 = new_value, 
    column_2 = new_value
WHERE condition_1

/*
ex. Update the values of the ContactName and City fields for the row whose CustomerId=1
*/
UPDATE Customers
SET ContactName = 'Christian Bale', City= 'Gotham'
WHERE CustomerID = 1;
```

***

## Deleting Rows

### > DELETE

* used to delete existing records in a table.
* The _**`WHERE`**_ clause specifies which record(s) should be deleted.
* If you omit the _**`WHERE`**_ clause, **all records** in the table will be deleted.

```sql
/* syntax */
DELETE FROM mytable
WHERE condition_1

/* clear table */
DELETE FROM mytable

/* ex. Remove all rows whose Brand=Porsche */ 
 DELETE FROM Cars
 WHERE Brand='Porsche';
```

***

## Creating Tables

### > CREATE TABLE

* used to create a new table in a db
* add a **IF NOT EXISTS** clause to avoid SQL errors.

```sql
/* Basic Syntax */
CREATE TABLE IF NOT EXISTS table_name (
  column1 datatype,
  column2 datatype,
	....
); 

/* Extra Optional Syntax: */
CREATE TABLE IF NOT EXISTS table_name (
  column1 datatype TableConstraint DEFAULT default_val,
  column2 datatype TableConstraint DEFAULT default_val,
 	....
);

/* Ex. */
CREATE TABLE movies (
    id INTEGER PRIMARY KEY,
    title TEXT,
    director TEXT,
    year INTEGER, 
    length_minutes INTEGER
);
```

* [Data Types Reference](https://www.w3schools.com/sql/sql\_datatypes.asp)
* [Constraint Reference](https://sqlbolt.com/lesson/creating\_tables)

**Create Table Using Another Table**

* You can also create a copy of an existing table using _**`CREATE TABLE`**_
* The new table gets the same column definitions. All columns or specific columns can be selected.
* If you create a new table using an existing table, the new table will be filled with the existing values from the old table

```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```

***

## Altering Tables

### > ALTER TABLE

* used to add, delete, or modify columns in an existing table.
* also used to add and drop various constraints on an existing table.

### 1. _Adding Columns_ - ADD

* required: column **name** and **datatype**
* optional: table **constraints** and **default** values.

```sql
/* Basic Syntax */
ALTER TABLE mytable
ADD new_column datatype; 

/* Optional Syntax */
ALTER TABLE mytable
ADD new_column dataType optionalTableConstraint
    DEFAULT default_value;
```

### 2. _Removing Columns_ - DROP COLUMN

* Dropping columns is as easy as specifying the column to drop, however, some databases (ie. SQLite) don't support this feature.
* Instead, you may have to create a new table and migrate the data over

```sql
/* Syntax */
ALTER TABLE mytable
DROP COLUMN column_to_be_deleted;
```

### 3. _Renaming Columns_ - RENAME TO

```sql
/* Syntax */
ALTER TABLE mytable
RENAME TO new_table_name;
```

### 4. _Alter Column Datatype_ - (varies from rdbms to rdbms)

***

## Dropping Tables

### > DROP TABLE

* used to remove an entire table including all of its data
* differs from the **DELETE** statement in that **DROP TABLE** also removes the table schema from the db entirely
*   use with **IF EXISTS** to avoid errors

    ```sql
    DROP TABLE IF EXISTS mytable;
    ```

***

### > UNION

* used to combine the result-set of two or more _**`SELECT`**_ statements
*   Every _**`SELECT`**_ within _**`UNION`**_ must have the same # of columns of the same data types and in the same order.

    ```sql
    /* syntax */
    SELECT column_name FROM table1
    UNION
    SELECT column_name FROM table2; 
    ```
*   The _**`UNION`**_ operator selects only distinct values by default. To allow duplicate values, use _**`UNION ALL`**_:

    ```sql
    /* syntax */
    SELECT column_name FROM table1
    UNION ALL
    SELECT column_name FROM table2;
    ```

### > EXISTS

*   used to test for the existence of any record in a subquery

    ```sql
    SELECT column_name
    FROM table_name
    WHERE EXISTS
    ```

### > SELECT INTO

*   copies all (or some) columns from one table into a new table:

    ```sql
    /* swap out '*' for 'col1, col2, ...' to copy only some columns into a new table */
    SELECT * INTO new_table
    FROM old_table
    WHERE condition_1;

    ```

### > CASE ... END

* The _**`CASE`**_ statement goes through conditions and returns a value when the first condition is met (like an if-then-else statement).
* Once a condition is true, it will stop reading and return the result.
* If no conditions are true, it returns the value in the _**`ELSE`**_ clause

```sql
/* Basic Syntax */
 CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;

/* Ex. */
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'Quantity is greater than 30'
    WHEN Quantity = 30 THEN 'Quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

### > CREATE DATABASE

*   used to create a new SQL db

    ```sql
    CREATE DATABASE db_name
    ```

### > DROP DATABASE

*   used to drop an existing SQL database (use w/ IF EXISTS for safety)

    ```sql
    DROP DATABASE IF EXISTS existing_db_name
    ```

### Constraints

* SQL constraints are used to specify rules for the data in a table.
* They're used to limit the type of data that can go into a table. (for accuracy and reliability reasons).
* If there is any violation between the constraint and the data action, the action is aborted.
* Constraints can be applied to a column or an entire table.
* The following constraints are commonly used:

|  Constraint  |                             Description                             |
| :----------: | :-----------------------------------------------------------------: |
|   NOT NULL   |              ensures that column can't have NULL value              |
|    UNIQUE    |          ensures that all values in a column are different          |
|  PRIMARY KEY | combo of NOT NULL + UNIQUE. Uniquely identifies each row in a table |
|  FOREIGN KEY |       prevents actions that would destroy links between tables      |
|     CHECK    |     ensures that values in a column satisfy a specific condition    |
|    DEFAULT   |                  sets a default value for a column                  |
| CREATE INDEX |       create and retrieve data from the database very quickly       |

```sql
CREATE TABLE Persons (
    ID int NOT NULL AUTO_INCREMENT,
    LastName text NOT NULL,
    FirstName text NOT NULL DEFAULT 'Joe',
    Age int
  	PRIMARY KEY (ID)
	  CHECK (Age>=18)
); 
```

***

### Single line commentz: `-- here`

```sql
-- this and that and this
```

### Multi line commentz: `/* here */`

```sql
/*
this
and that
and this
*/
```
