# FunWithSQL
Some notes and useful code I am using with SQL

* Having

In SQL, aggregate functions can't be used in WHERE clauses. For example, the following query is invalid:


```
SELECT release_year
FROM films
GROUP BY release_year
WHERE COUNT(title) > 10;

```


instead, use

```
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;
```



information_schema is a meta-database that holds information about your current database

information_schema has multiple tables you can query with the known SELECT * FROM syntax:

    tables: information about all tables in your current database
    columns: information about all columns in all of the tables in your current database 
    
    
 the 'public' schema, which is specified as the column table_schema of the tables and columns tables. The 'public' schema holds information about user-defined tables and databases. The other types of table_schema hold system information
 
 
 Example to get table names from data base using public info (notice no mention of table name, as we are looking for all table names)
 
 ```
 -- Query the right table in information_schema
SELECT table_name 
FROM information_schema.tables
-- Specify the correct table_schema value
WHERE table_schema = 'public';
```

To get the names and data types of columns in a specific table

```
-- Query the right table in information_schema to get columns
SELECT column_name, data_type 
FROM information_schema.columns 
WHERE table_name = 'university_professors' AND table_schema = 'public';
```

To create tables

```
CREATE TABLE weather (
clouds text,
temp numberic,
weather_station char(5));
```


to add an additional column after ctrating an empty table

```
ALTER TABLE table_name
ADD COLUMN column_name data_type;
```

* Data types  
text         | variable text  
varchar(n)   | up to n charachters  
char(n)      | fixes n character  
boolean      | yes, no, Null  
date, time, timestamp |    
numberic (n,m)  | n = 3, m =2 gives 3 digists with 2 sigfigs  
integer |      





Truncate a column by converting the data type to up to x (retain a substring x of every value in the column)

```
ALTER TABLE table_name
ALTER COLUMN column_name
TYPE varchar(x)
USING SUBSTRING(column_name FROM 1 FOR x)
```
