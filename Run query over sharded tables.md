Iterates over dates and runs query over each sharded table in set:
``` sql
DECLARE query STRING; 
FOR day IN (
  SELECT
    FORMAT_DATE("%Y%m%d", d) AS day
  FROM
    UNNEST(GENERATE_DATE_ARRAY('2022-07-28','2022-09-11',INTERVAL 1 day)) AS d
  ) 
DO
  SET query = CONCAT("CREATE TABLE project.dataset.sharded_table_",day.day," COPY project.dataset_2.sharded_table_",day.day);
  EXECUTE IMMEDIATE query;
END FOR;
```
#bigquery #sql #sharded
