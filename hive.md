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
4. Upload new TSV file to hadoop so we can insert into new table





References:
- https://bigdataprogrammers.com/load-csv-file-into-hive-orc-table/
