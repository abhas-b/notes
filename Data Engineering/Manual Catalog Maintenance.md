
#aws 
[[Athena]] [[Glue]]

 We can create table and update it in catalog as well.
 This approach is used when you want a schema that's different from what crawler came up with.

```
CREATE EXTERNAL TABLE 'iris_manual' (
'sepal_length' double,
'sepal_wdith' double
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
LOCATION 's3://...'
TBLPROPERTIES ('skip.header.line.count'='1', 'typeOfData'='file', 'classification'='csv')
```