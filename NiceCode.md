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
