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
