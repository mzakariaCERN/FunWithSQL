-- Create a tables with group by, showing percentages

```
SELECT client_browser, count(*), ((count(*) * 100.0
                          / sum(count(*)) OVER ())) AS percent
FROM  Table
GROUP  BY 1
ORDER  BY 2 Desc;
```


## Example how to generate a simple table with Impala

[line](https://www.cloudera.com/documentation/enterprise/5-8-x/topics/impala_create_table.html)

```
drop table mz_Table_Delete;

CREATE TABLE mz_Table_Delete (x INT, y STRING);
INSERT INTO mz_Table_Delete VALUES (1, 'one'), (2, 'two'), (3, 'three');

select * from mz_table_delete
```


BETWEEN is inclusive and can replace >= and <=

IN (1, 2, 3) can replace multiple or satatements

to search for NULL we use is NULL or IS NOT NULL

LIKE is for non-exact match
WHERE name like 'Mo%'
% is greedy free card
_ is on character card

we can also use NOT LIKE to exclude the pattend

names that don't start with M
WHERE name NOT LIKE 'M%'
