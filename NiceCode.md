-- Create a tables with group by, showing percentages

```
SELECT client_browser, count(*), ((count(*) * 100.0
                          / sum(count(*)) OVER ())) AS percent
FROM  Table
GROUP  BY 1
ORDER  BY 2 Desc;
```
