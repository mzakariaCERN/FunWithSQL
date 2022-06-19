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


To set a column as a primary kye (in postgres)

```
ALTER TABLE table_name
ADD CONSTRAINT some_name PRIMARY KEY (column_name)
```

You can also have multiple columns in the bracket. But generally speaking, the fewer columns in a primary kye, the better.

Ever table should have a primary key identified


## Surrogate keys
This is a key that is not a column that exists in the table. We create it eather by making an index, or by combining two columns. 

Why would you need that? 
1. Primary key should be based on as few columns as possible
2. They key should now change in time. Some columns might be good keys, but there is a chance they would change in time

There is a specific data type for surrogate keys in postgres, it is called Seriel

two ways to add a surrogate key

```
-- Add the new column to the table
ALTER TABLE professors 
add column id serial primary key;
```

-- Make id a primary key and rename it to professors_pkey
```
ALTER TABLE professors 
ADD CONSTRAINT professors_pkey PRIMARY KEY (id);
```

Another way is to combine two exisisting columns to get a surrogate key
```
-- Count the number of distinct rows with columns make, model
SELECT COUNT(DISTINCT(make, model)) 
FROM cars;

-- Add the id column
ALTER TABLE cars
ADD COLUMN id varchar(128);

-- Update id with make + model
UPDATE cars
SET id = CONCAT(make, model);

-- Make id a primary key
alter table cars
add constraint id_pk primary key(id);

-- Have a look at the table
SELECT * FROM cars;
```

A Foreign Key (FK) in a table points to a primary key of another table.
- FK domain and data type must be the same for PK. 
- If you added a data point to the table with an FK entry that is not within the PK values you will get an error (FK constraint)

FK is not an actual key: duplicates and null values are allowed.

In your database, you want the professors table to reference the universities table. You can do that by specifying a column in professors table that references a column in the universities table.

The syntax for that looks like this:
```
ALTER TABLE a 
ADD CONSTRAINT a_fkey FOREIGN KEY (b_id) REFERENCES b (id);
```
Table a should now refer to table b, via b_id, which points to id. a_fkey is, as usual, a constraint name you can choose on your own. 

Pay attention to the naming convention employed here: Usually, a foreign key referencing another primary key with name id is named x_id, where x is the name of the referencing table in the singular form.

```
-- Add a foreign key on professors referencing universities
ALTER TABLE professors 
ADD CONSTRAINT professors_fkey FOREIGN KEY (university_id) REFERENCES universities (id);
```

While foreign keys and primary keys are not strictly necessary for join queries, they greatly help by telling you what to expect. For instance, you can be sure that records referenced from table A will always be present in table B – so a join from table A will always find something in table B. If not, the foreign key constraint would be violated.


The syntax for declaring a foreign key while adding a new column is as follows:
```
ALTER TABLE table_name
ADD COLUMN column_name data_type REFERENCES other_table_name (other_column_name);
```


```

-- Update professor_id to professors.id where firstname, lastname correspond to rows in professors
UPDATE affiliations
SET professor_id = professors.id
FROM professors
WHERE affiliations.firstname = professors.firstname AND affiliations.lastname = professors.lastname;
```


* Referential Integrity

Means that when a record referencing another table must reer to an existing record in that table. We enforce this using Foreign Keys

When A is referenced by B. We can violate referential integrity in 2 ways:
1. If you delete record in B that has a reference in A
2. if you insert a record in A that doesn't have a reference in B

To identify the constraints in you table use the following:
```
-- Identify the correct constraint name
SELECT constraint_name, table_name, constraint_type
FROM information_schema.table_constraints
WHERE constraint_type = 'FOREIGN KEY';
```

Altering a key constraint doesn't work with ALTER COLUMN. Instead, you have to DROP the key constraint and then ADD a new one with a different ON DELETE behavior.

For deleting constraints, though, you need to know their name. This information is also stored in information_schema.
