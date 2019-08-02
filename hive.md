### How do I see how a table got created?
```show create table foo_schema.foo_table;```

### How do I transfer Hive data from one cluster to another?
**If the table is small you might can use this method**

1. Extract the data from Hive into a TSV file. 
  - ```hive -e 'select * from foo_schema.foo_table' > /home/gdouser/stirling/foo_table_extract.tsv```
2. Server copy it from your edge sever box to your local machine
  - ```scp -prq  myuser@111.111.111.111:/home/myuser/stirling/foo_table_extract.tsv /Users/stirlingw/Projects/mycoolproject/ ```
3. Copy from your local machine to the new edge server box
  - ```scp -prq  /Users/stirlingw/Projects/mycoolproject/foo_table_extract.tsv mynewuser@22.222.222.222:/home/mynewuser/stirling/foo_table_extract.tsv ```
4. Make a new directory for the TSV file to upload to in HDFS
 - hadoop fs -mkdir foo_extract
5. Upload new TSV file to new cluster hadoop so we can insert into new table
  - `hadoop fs -put /home/mynewuser/stirling/foo_table_extract.tsv hdfs://newcoolserver/user/hadoopawesomeuser/foo_extract` 
6. Check to see if the file made it into HDFS
  - hadoop fs -ls hdfs://newcoolserver/user/hadoopawesomeuser/foo_extract
7. Create a tempory Hive Table for the new file to get uploaded to:
  - In the old edge server box in hive run `hive -e "show create table rmd_prosp_dev.rm_up_mid_vertical;"`
    - This will give you the hive table create statment needed for your new box
  - Use the create statement to create the temp table on your new box
```
```





References:
- https://bigdataprogrammers.com/load-csv-file-into-hive-orc-table/
