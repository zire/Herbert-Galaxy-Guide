# Command Comands for PostgreSQL

## Convention

A few conventions to follow:

1. Use `singular` form for database
2. Use `plural` form for table

## Basic Usage on Mac

List all available databases from console

```
$ psql -l
```

Connect to a database to arrive at psql prompt

```
$ psql XXX
```

List all available databases from postgresql prompt

```
\l
```

Create a database `startup` with default settings

```
CREATE DATABASE startup;
```

Connect to this newly created database

```
\c startup
```

List all tables from current database

```
\dt
```

Create a table

```
CREATE TABLE my_first_table (
	ID serial primary key,
	first_column text,
	second_column int,
	third_column, numeric
);
```

Describe a table

```
\d my_first_table
```

Rename a table

```
ALTER TABLE table_name
RENAME TO new_table_name;
```

Delete a table

```
DROP TABLE table_name;
```

Rename a column

```
ALTER TABLE table_name
RENAME COLUMN column_old_name TO column_new_name;
```

Change data type of a column

```
ALTER TABLE table_name
ALTER COLUMN column_name TYPE new_data_type;
```

Remove a column from a table

```
ALTER TABLE table_name
DROP COLUMN column_name;
```

Add a column to a table

```
ALTER TABLE table_name
ADD COLUMN new_column_name data_type;
```

View data from a table

```
SELECT * FROM my_table;
```

Or view data with selected columns only

```
SELECT col_first, col_sec FROM my_table
```

## Queries in PostgreSQL

Use `WHERE` to display the records that meet certain condition

```
SELECT * FROM my_table 	WHERE first_column = 'China'
```

Use `COUNT` to return the number of rows returned by a `SELECT` statement

```
SELECT COUNT(*) FROM my_table WHERE first_column = 'China'
```

Use `DISTINCT` with `COUNT` to return the number of unique non-null values in the column

```
SELECT
	COUNT (DISTINCT some_column_name)
FROM
	table_name;
```

Use `GROUP BY` and `SORT BY` to get a pivot-table-esque summary

```
SELECT
	country,
	COUNT (country)
FROM
	my_table
GROUP BY
	country
ORDER BY
	COUNT (country) DESC;
```
Without `DESC`, by default the result will be displayed in ascending order, or `ASC`. 

## Import Excel Data into a Table

1. Save the Excel data file into `csv` format, delimited by comma. Say, this raw data file contains 6 columns. 

2. Create a table in the database. An index column `id` is added using data type `serial`.

	```
CREATE TABLE cbi_unicorn_list_20190118 (
	id serial,
	company_name text,
	valuation_$m numeric,
	category text,
	country text,
	total_disclosed_funding_$m numeric,
	select_investors
);
```

3. Use `copy` command to import the csv file into PostgreSQL table

	```
	COPY cbi_unicorn_list_20190118 (
		company_name,
		valuation_$m,
		category,
		country,
		total_disclosed_funding_$m,
		select_investors
	)
	FROM 'path-to-file' DELIMITER ',' CSV HEADER;
	```
Note that: 1) `copy` might not work if user does not have admin permission. Use `\copy` instead. 2) `HEADER` keyword indicates that the CSV file contains a header line with column names. PostgreSQL will ignore the first line, which is the header line of the file. If `CSV HEADER` is omitted, every line in the CSV file will be imported including the first line. 

## Other Tips

Changing position of column is a tricky business. Suggest to recreate a new table with the modified sequence as [this SO article mentioned](https://stackoverflow.com/questions/126430/is-it-possible-to-change-the-natural-order-of-columns-in-postgres).

## Data Types

For string, use `text` rather than `char(n)`, or `varchar(n)`, as suggested by [this SO article](https://stackoverflow.com/questions/4848964/postgresql-difference-between-text-and-varchar-character-varying).

## Reference

[Official PostgreSQL 11.6 Documentation](https://www.postgresql.org/docs/11/index.html)

[table-naming-dilemma-singular-vs-plural-names](https://stackoverflow.com/questions/338156/table-naming-dilemma-singular-vs-plural-names)

[Import CSV File Into PostgreSQL Table](http://www.postgresqltutorial.com/import-csv-file-into-posgresql-table/)

***

[Back to HitichHikder's Guide by Herbert](README.md)