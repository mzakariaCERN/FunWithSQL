-- Create a tables with group by, showing percentages

SELECT client_browser, count(*), ((count(*) * 100.0
                          / sum(count(*)) OVER ())) AS percent
FROM  ds_dev01.ds_eu_c360_webblock_feature_view
GROUP  BY 1
ORDER  BY 2 Desc;
