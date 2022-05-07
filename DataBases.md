We introduce constrains in data bases to get better data quality assurance. These constraints define the data model 

type of constrains
1. Attribute Constrains (data type constrain)
2. Key Constrains
3. Referential Integrity Constrain (using a foreign key)



## key constraints
a key: is an attribute or a group of them that define every record uniquely
a super key, is an attribute or a set of attributes that can be removed without losing the uniqueness of the records
so a minimal super key needed to preserve uniqueness of every record is called a key

we can study keys using this SQL query
```
SELECT COUNT(DISTINCT(column_a, column_b, ...))
FROM table;
```

and compare it to
```
SELECT count(*)
FROM table;
```

There's a very basic way of finding out what qualifies for a key in an existing, populated table:

    1. Count the distinct records for all possible combinations of columns. If the resulting number x equals the number of all rows in the table for a combination, you have discovered a superkey.

    2. Then remove one column after another until you can no longer remove columns without seeing the number x decrease. If that is the case, you have discovered a (candidate) key.